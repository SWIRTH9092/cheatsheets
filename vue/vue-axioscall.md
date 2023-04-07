##### Vue - AXIOS

- install axios
    - terminal:  npm install axios

-   in the .env.local file  code the URL

    ```
    VUE_APP_ROOT_API=https://sw-goalmgr-bkend.onrender.com
    ```

-   in the script tag
    -   import axios
    -   under methods is an example of an api call
        - note: local storage is used to pass data between views

```
<script>

import axios from "axios";

export default {
import axios from "axios";
export default {
    methods: {
        async submitLogin(e) {
            const url = process.env.VUE_APP_ROOT_API + '/auth/login'
            await axios
                .post(url, {
                u_Userid: this.u_Userid,
                u_Password: this.u_Password
            })
                .then((response) => {
                    this.isLoggedIn = true;
                    localStorage.setItem("isLoggedIn", "true");
                    this.u_RootKey = response.data.u_RootKey;
                    localStorage.setItem("u_RootKey", this.u_RootKey);                  
                    router.push({ name: "GoalListView" });
            })
                .catch((error) => {
                    this.isLoggedIn = false;
                    localStorage.setItem("isLoggedIn", "false");
                    this.loginError = `create Unsuccessful - ${error}`;
            });
        }
    }
}
</script>
```