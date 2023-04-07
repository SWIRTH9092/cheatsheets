##### Vue - fetch

- Helpful Links:
    - https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch

- example of using fetch with sending data
    - the body data in the example below being sent needs to be sent using:  JSON.stringify(loginData)

        ```
        const url = process.env.VUE_APP_ROOT_API + '/auth/login'
        const loginData =   { 
            u_Userid: this.u_Userid,
            u_Password: this.u_Password
            };                      
            await fetch (url, {
                method: "POST",
                headers: {
                    "Content-Type": "application/json",
                },
                body: JSON.stringify(loginData),
            })
            .then(response => response.json())
            .then(data => {
                this.isLoggedIn = true;
                localStorage.setItem("isLoggedIn", "true");                         
                this.u_RootKey = data.u_RootKey;
                localStorage.setItem("u_RootKey", this.u_RootKey);                  
                router.push({ name: "GoalListView" });
            })
            .catch((error) => {
                this.isLoggedIn = false;
                localStorage.setItem("isLoggedIn", "false");
                this.loginError = `login Unsuccessful - ${error}`;
            });
        ```

- "get" example of using fetch for a git request  with a param
    ```
    const url = process.env.VUE_APP_ROOT_API + '/goallist/index/' +     this.u_RootKey

    await fetch (url)
        .then(response => response.json())
        .then(data => {
            this.goallists = data;
        })
        .catch((error) => {
            this.loginError = `Getting Data Unsuccessful - ${error}`;
    });
    ```
- "post" example of using fetch for create 
    ```
        const createData = this.createGoalList
        const url = process.env.VUE_APP_ROOT_API + '/goallist/create'
        await fetch (url, {
            method: "POST",
            headers: {
                "Content-Type": "application/json",
                },
                body: JSON.stringify(createData)
            ,
        })
            .then(response => response.json())
            .then (data => {
                // blank out create fields
                this.createGoalList.gl_URootKey = ''
                this.createGoalList.gl_Name = ''
                this.createGoalList.gl_Stat = ''
                this.createGoalList.gl_Description = ''
                this.createGoalList.gl_StartDate = this.currentDate
                this.createGoalList.gl_EndDate = this.currentDate
                // add the goal to the list
                this.goallists.push(data)                    
            })
            .catch((error) => {
                this.createError = error
        });
    ```
- "put" example of using fetch for upate
    ```
        const bodyToUpdate = this.updateGoalList
        const url = process.env.VUE_APP_ROOT_API + '/goallist/update/' + docToUpate
        await fetch(url, {
            method: "PUT",
            headers: {
                "Content-Type": "application/json",
            },
            body: JSON.stringify (bodyToUpdate),
        })
        .then(() => {
            localStorage.removeItem("updateGLData")
            router.push( {name: "GoalListView"} )  
            })
        .catch((error) => {
            this.updateError = error;
        })
    ```

- "delete" example of using fetch for delete
    ```
        async removegoallist(item, i) {
            const url = process.env.VUE_APP_ROOT_API + '/goallist/delete/'+ item._id
            if (confirm("Are you sure you want to delete this goal from your list?")) {
                await fetch (url, {
                    method: "DELETE"
                })
                .then (response => {
                    if (response.ok) {
                        this.goallists.splice(i, 1); 
                    } else {
                        throw new Error("Error in delte")
                    }   
                })
                .catch((error) => {
                    this.deleteError = error
                })   
            } 
        }
    ```