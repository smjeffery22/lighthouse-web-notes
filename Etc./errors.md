`permission denied for relation items`
  * database related error
  * ran into this error during the midterm project when trying to establish database connection in the routes file
  * issue was that the user information in the database connection setup was not correct
  * resolved by correcting the user information in .env file

`TypeError: usersQueries.getItems is not a function`
  * ran into this error during the midter project when trying to export query file and function and import into router file
  * issue was that I was not exporting as an object
  * fixed by exporting as an object
    ```js
    // error
    module.exports = getItems;

    // error fixed
    module.exports = { getItems };
    ```
