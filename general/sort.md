### Sort

-  Resources

    - Steve Griffith - Sorting Complex Objects in Javascript:  https://www.youtube.com/watch?v=AmQ1OX7XBJw

#### Sort Objects

###### Object String Sorts


- Function:
    ```
        // Object Sort by Stirng - Name
        //   Input:  an array occurence that contain the object gl_Name
        //   output: Return: 1   - a.gl_ Name is > b.gl_ Name
        //           Return: -1  - a.gl_ Name is < b.gl_ Name
        //           Return: 0   - the values are equal

        export function byName(a,b) {
            if (a.gl_Name > b.gl_Name ) {
                return 1; 
            } else if (a.gl_Name < b.gl_Name)  { 
                return -1;
            } else {
                return 0;
            }
        }
    ```

- Function Call:
    ```
        const work_InProcess = this.goallists_InProcess.sort(byName)
    ```

##### Object Integer Sort

- Function
    ```
        // Object Sort by Interger - gl_SortOrder
        //   Input:  an array occurence that contain the object gl_SortOrder
        //   Process: to process the sort order correctly, the sort order must be 
        //            converted to an integer
        //   output: Return parseInt(a.gl_SortOrder) - parseInt(b.gl_SortOrder)
        export function bySortOrder(a,b) {

            return parseInt(a.gl_SortOrder) - parseInt(b.gl_SortOrder)

        }
    ```

- Function Call
    ```
        const work_InProcess = this.goallists_InProcess.sort(bySortOrder)
    ```


##### Object Date Sort - by year, month, day
- Function
    ```
        // Object Sort by date - gl_StartDate
        //   Input:  an array occurence that contain the object gl_StartDate
        //   Process: to process the date correctly, the date must be converted to a date which
        //            give the date a timestamp
        //   output: Return new Date (a.gl_StartDate).valueOf() - new Date (b.gl_StartDate).valueOf();

        export function byStartDate(a,b) {
            return new Date (a.gl_StartDate).valueOf() - new Date (b.gl_StartDate).valueOf();
        }

    ```
- Function Call
    ```
        const work_InProcess = this.goallists_InProcess.sort(byStartDate)
    ```    

##### Object Date Sort - month, day

- Function
    ```
        // Object Sort by date - gl_StartDate by Month, Day
        //   Input:  an array occurence that contain the object gl_StartDate
        //   Process: to process the date correctly, the date must be converted to a date.  then
        //             the data is sorted into month day order (bypassing the year)
        //   output: 

        export function byStartDateMonthDay(a,b) {
            // by month and then by day
            let d1 = new Date(a.gl_StartDate);
            let d2 = new Date(b.gl_StartDate);
            if (d1.getUTCMonth() > d2.getUTCMonth()) {
                return 1;
            } else if (d1.getUTCMonth() < d2.getUTCMonth()) {
                return -1
            } else {
                return d1.getUTCDate() - d2.getUTCDate()
            }

        }
    ```

- Function Call
    ```
        const work_InProcess = this.goallists_InProcess.sort(byStartDateMonthDay)
    ``` 