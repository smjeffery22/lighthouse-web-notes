### JSON

JSON (JavaScript Object Notation) is a data format that underpins many modern web services and it a subset of the JS language.
JSON is built on two structures:

- A collection of *name:value* pairs
- An ordered list of values

```js
{
  "name": "New York City",
  "boroughs": [
    "Manhattan",
    "Queens",
    "Brooklyn",
    "The Bronx",
    "Staten Island"],
  "population": 8491079,
  "area_codes": [212, 347, 646, 718, 917, 929],
  "position": { "lat": 40.7127, "lng": -74.0059 }
}
```

- *Keys* are always double-quoted *"strings"*
- Values can be numbers, strings, objects, arrays, booleans and null

**Serialization**
The process of serialization *coverts objects* (or data structures) into a *format that can be stored or transmitted between computers*(typically as a *string of text*)

- Opposite is deserialization (string -> object)

`JSON.parse():` Parse a string as JSON, optionally transform the produced value and its properties, and return the value.

`JSON.stringify():` Return a JSON string corresponding to the specified value, optionally including only certain properties or replacing property values in a user-defined manner.

```js
const jsonString = '{"a": 1, "b": 2, "foo": "bar"}';
const obj = JSON.parse(jsonString);
// obj = { a: 1, b: 2, foo: "bar"}
const obj2 = JSON.stringify(obj);
// obj2 = '{"a": 1, "b": 2, "foo": "bar"}'
```