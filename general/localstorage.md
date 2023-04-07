##### Local Storage

- Helpful Links:
    - https://www.w3schools.com/jsref/prop_win_localstorage.asp
    - https://blog.logrocket.com/localstorage-javascript-complete-guide/

- Local storage is in JSON format
- Location storage is stored on the browser under applications

- Local Storage objects
    - localStorage.setItem() - adds an item
    - localStorage.getItem() - retrieves an item 
    - localStorage.removeItem() - removes an item

- setItem Example - adding to local storage
```
    //**  1st parameter is the tag name
    //**  2nd parameter is the data value - object

    //**   Setting local storage using a single object value

        localStorage.setItem("isLoggedIn", "true");
        localStorage.setItem("u_RootKey", this.u_RootKey); 

    //**   Setting local storage using a data value with
    //**   an object data structure.  Note: the 
    //**   JSON.stringufy method is used on the value object

            updateGoalList: {
                _id: '',
                gl_URootKey: '',
                gl_Name: '',
                gl_Stat: '',
                gl_Description: '',
                gl_StartDate: '',
                gl_EndDate: '',
                gl_SortOrder: '',

            localStorage.setItem('updateGLData', JSON.stringify(updateGoalList))

```

- getItem Example - retrieving from local storage
```

    //**  the only parameter is the tag name

    //* Example of retrieving a single object
    this.u_RootKey = localStorage.getItem('u_RootKey')
    this.isLoggedIn = localStorage.getItem('isLoggedIn')

   //* Example of retrieving an object data structure.

        //**  empty array defined to store the data 
        
            goallist = []

        //**  JSON.parse is used to unparse the JSON format 
           goallist = JSON.parse(localStorage.getItem("updateGLData"))
```

removeItem Example - deleting from local storage
```
    //**  the only parameter is the tag name  
    
    localStorage.removeItem("updateGLData")
```