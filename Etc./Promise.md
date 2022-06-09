# Promise

## Chained then
  * **Anything returned in `.then` returns in the next `.then`**
  * `.then` returns a promise
  * `.catch` also returns a promise
    * `.catch` not only catches promise errors, it also catches JS errors
    ```js
    pool.query(sql)
      .then(res => {
        console.log('then 1:', res.rows);
        return 5;
      })
      .then(res => {
        console.log('then 2:', res.rows); //will print 5
      })
    ```
  * `.finally(() => { console.log('finally!') })`
    * include `pool.end()` inside to end


## 3 Parts of promise
  1. `.then`
  2. `.catch`
  3. `.finally`