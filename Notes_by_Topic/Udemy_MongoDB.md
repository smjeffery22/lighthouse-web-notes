# Database

  - MongoDB: https://docs.mongodb.com/manual/
  - Mongoose: https://mongoosejs.com/docs/api/model.html

`Why Database?`

  - Databases can handle **large amounts** of data **efficiently** and store it **compactly**
  - Easy insertion, querying and updating of data
  - Security features and control over access to data

`SQL vs. No-SQL`

**SQL Databases**

  - Structured Query Language (SQL) databases are relational databases (basic syntax they both share)
  - Pre-define a schema of tables before inserting anything into the database
    - Tables are connected and referenced to one another

**No-SQL Database**

  - Do not need pre-defined schema of tables, rather data can be stored in some format such as JSON
    - More flexibility

## MongoDB

  - Commonly used with Node and Express
    - MEAN / MERN stacks

  - MongoDB plays particularly well with JS

`db` current db

`show dbs` show database names

`use <db_name>` set current db; if it does not exist, makes a new db

`show collections` show collections in current db

### BSON (Binary JSON)

  - JSON is a text-based format and text parsing is slow
  - JSON only supports a limited number of data types

  - BSON's binary structure encodes type and length information, which allows it to be parsed much more quickly
    - JSON-looking syntax, but also saves as something that is a lot more compact
  - Supported data types:
    - String
    - Boolean
    - Number
      - Integer, Float, Long, Decimal, etc.
    - Array
    - Date
    - Raw Binary

### Insert Documents

  - Data is inserted into collections (i.e. entities)
    - If collection does not exist, it is created upon insertion

`db.collection_name.insert({name: "Jeffery", age: 22, nationality: "Korean"})` insert one/many data into collection - primary key (id) automatically created

`db.collection_name.find()` list objects in collection

### Query Documents

`db.collection_name.find({nationality: "Korean", age: 22})` find all that matches the condition
  - returns a cursor

`db.collection_name.findOne({nationality: "Korean"})` find only one that matches the condition
  - returns the document

`db.dogs.find({'personality.childFriendly': true, age: 10})`
  - 'personality.childFriendly' to access childFriendly that is nested inside personality

#### Comparison Operators

  - https://docs.mongodb.com/manual/reference/operator/query-comparison/#std-label-query-selectors-comparison

*$eq* matches values that are equal to a specified value.

*$gt* matches values that are greater than a specified value.

*$gte* matches values that are greater than or equal to a specified value.

*$in* matches any of the values specified in an array.

*$lt* matches values that are less than a specified value.

*$lte* matches values that are less than or equal to a specified value.

*$ne* matches all values that are not equal to a specified value.

*$nin* matches none of the values specified in an array.

#### Logical Operators

  - https://docs.mongodb.com/manual/reference/operator/query-logical/

*$and* joins query clauses with a logical AND returns all documents that match the conditions of both clauses.

*$not* inverts the effect of a query expression and returns documents that do not match the query expression.

*$nor* joins query clauses with a logical NOR returns all documents that fail to match both clauses.

*$or* joins query clauses with a logical OR returns all documents that match the conditions of either clause.

#### Array Update Operators

  - https://docs.mongodb.com/manual/reference/operator/update/pull/

*$pull* removes from an existing array all instances of a value or values that match a specified condition
  - `{ $pull: { <field1>: <value|condition>, <field2>: <value|condition>, ... } }`

### Update Documents

`db.collection.updateOne(filter, update, options)`
`db.collection.updateMany(filter, update, options)`

`db.collection_name.updateOne({name: "Jeffery"}, {$set: {age: 29, wearGlasses: true}, $currentDate: { lastModified: true }})`
  - *$set* operator used to update/replace the value of a field
  - *$currentDate* operator to add modified date
  - field-value can be updated or added

`db.collection_name.updateMany({nationality: "Korean"}, {$set: {isAsian: true}})`
  - updateMany updates all documents that match the specified filter

### Delete Documents

`db.collection.deleteMany()`
`db.collection.deleteOne()`
  
  - Similar to query documents

## Mongoose

  - **ODM (Object Data/Document Mapper)**
    - ODMs like Mongoose map documents coming from a database into usable JS objects
    - To interact with Mongo database more easily from JS

  - `npm i mongoose` to install

  - To connect database:

    ```js
    const mongoose = require('mongoose');

    mongoose.connect('mongodb://localhost:27017/movieApp')
      .then(() => console.log('Connection established!'))
      .catch(err => console.log(`Error: ${err}`));
    ```

    ```js
    const mongoose = require('mongoose');

    mongoose.connect('mongodb://localhost:27017/yelp-camp');

    const db = mongoose.connection;

    db.on('error', console.error.bind(console, 'connection error:'));
    db.once('open', () => {
      console.log('Database connected!');
    });
    ```

    - Mongoose is set up so that it allows to start using the models immediately without waiting for the connection to be established
      - *Operation buffering*
      
    - **.on**
      - if there is an error, the on callback would run which would result into printing the error in console
      - NodeJS-specific

    - **.once**
      - callback to be executed when the given event is generated
      - function will be called when the connection to mongodb is open (i.e. the connection is successful)

### Models

  - JS classes that we make with the assistance of Mongoose that represent information in a Mongo database
    - Represent information in some collection

  - Define **Schema** first

    ```js
    const movieSchema = new mongoose.Schema({
      title: String,
      year: Number,
      score: Number,
      rating: String
    })
    ```

  - Create a **Model**

    ```js
    const Movie = mongoose.model('Movie', movieSchema);
    const amadeus = new Movie({ title: 'Amadeus', year: 1986, score: 9.2, rating: 'R'});

    Movie.insertMany([
      { title: 'Amelie', year: 2001, score: 8.3, rating: 'R' },
      { title: 'Alien', year: 1979, score: 8.1, rating: 'R' },
      { title: 'The Iron Giant', year: 1999, score: 7.5, rating: 'PG' },
      { title: 'Stand By Me', year: 1986, score: 8.6, rating: 'R' },
      { title: 'Moonrise Kingdom', year: 2012, score: 7.3, rating: 'PG-13' },
    ])
      .then(data => {
        console.log('Data inserted!');
        console.log(data);
      })
    ```

    - *Model class* called Movie (const Movie)
    - String in bracket should be first-letter capitalized and singular
    - *Model* name is *Movie* and *collections* will be created called *movies*
    - *New instance of movie* can be created and saved in a variable (amadeus)


#### Finding and Updating

  ```js
  Movie.find({rating: 'PG-13'}).then(data => console.log(data))

  Movie.find({year: {$gte: 2015}}).then(data => console.log(data))

  Movie.updateOne(
    {title: 'Amadeus'},
    {year: 1984}
  )
    .then(res => console.log(res))

  Movie.updateMany(
    {title: {$in: ['Amadeus', 'Stand By Me']}},
    {score: 10}
  )
    .then(res => console.log(res))

  Movie.findOneAndUpdate(
    {title: 'The Iron Giant'},
    {score: 7.8},
    {new: true}
  )
    .then(m => console.log(m)) 

  Movie.deleteMany({year: {$gte: 1999}}).then(msg => console.log(msg))

  Movie.findOneAndDelete({title: 'Alien'}).then(m => console.log(m))
  ```

  - `.find()` returns a query object
    - thenable object

  - `.updateOne()` / `.updateMany()` / `.deleteOne()` / `.deleteMany()`
    - just returns how many things were modified

  - `.findOneAndUpdate()`
    - *{new: true}* to return object with updated data
      - default is false and returns data before update

  - `.findOneAndDelete()`
    - returns deleted object

#### Schema Validations

  - https://mongoosejs.com/docs/schematypes.html

  - **Schema Types**
    - String
    - Number
    - Date
    - Buffer
    - Boolean
    - Mixed
    - ObjectId
    - Array
    - Decimal128
    - Map
    - Schema

  - **Schema Types Options**
    - *required:* boolean or function, if true adds a required validator for this property
    - *default:* Any or function, sets a default value for the path. If the value is a function, the return value of the function is used as the default.
    - *select:* boolean, specifies default projections for queries
    - *validate:* function, adds a validator function for this property
    - *get:* function, defines a custom getter for this property using Object.defineProperty().
    - *set:* function, defines a custom setter for this property using Object.defineProperty().
    - *alias:* string, mongoose >= 4.10.0 only. Defines a virtual with the given name that gets/sets this path.
    - *immutable:* boolean, defines path as immutable. Mongoose prevents you from changing immutable paths unless the parent document has isNew: true.
    - *transform:* function, Mongoose calls this function when you call Document#toJSON() function, including when you JSON.stringify() a document.

```js
const productSchema = new mongoose.Schema({
	name: {
		type: String,
		required: true,
		maxlength: 20,
	},
	price: {
		type: Number,
		required: true,
		min: [0, 'Price cannot be negative'],
	},
	onSale: {
		type: Boolean,
		default: false,
	},
	categories: {
		type: [String],
		default: ['Cycling'],
	},
  qty: {
    online: {
      type: Number,
      default: 0
    },
    inStore: {
      type: Number,
      default: 0
    }
  },
  size: {
  type: String,
  enum: ['S', 'M', 'L']
  }
});

const Product = mongoose.model('Product', productSchema);

const bike = new Product({
	name: 'Bike Helmet',
	price: 19.5,
	categories: ['Cycling', 'Safety'],
});
bike
	.save()
	.then((data) => {
		console.log('Added');
		console.log(data);
	})
	.catch((err) => {
		console.log('Error');
		console.log(err);
	});

Product.findOneAndUpdate({ name: 'Tire Pump' }, { price: -19.5 }, { new: true, runValidators: true })
	.then((data) => {
		console.log('Added');
		console.log(data);
	})
	.catch((err) => {
		console.log('Error');
		console.log(err);
	});
```

  - *required* to require the field to be not empty
  - String can be inserted into Number type as long as it can be converted to number
  - If a field that is not defined in the schema is inserted, it doesn't get added
  - Validator may not be on when updating values
    - Set `runValidators: true` as an option when updating
  - Custom validator error message can be assigned
    - *min: [0, 'Price cannot be negative']*
  - `enum` validator to check for the values in the array

### Model Instance Methods

  - Instance method refers to a single object in the db
  - The keyword "this" in instance methods refers to a particular object in the database

```js
// instance method
productSchema.methods.toggleOnSale = function () {
  this.onSale = !this.onSale;
  return this.save();
}

// instance method
productSchema.methods.addCategory = function (newCat) {
  this.categories.push(newCat);
  return this.save();
}

const Product = mongoose.model('Product', productSchema);

const findProduct = async () => {
	const foundProduct = await Product.findOne({ name: 'Bike Helmet' });
  console.log(foundProduct);
  await foundProduct.toggleOnSale();
  console.log(foundProduct);
  await foundProduct.addCategory('Outdoors');
  console.log(foundProduct);
};

findProduct();
```

### Model Static Methods

  - Static methods are set to refer to the whole model
  - The keyword "this" refers to the whole model (i.e. Product)

```js
productSchema.statics.fireSale = function () {
	return this.updateMany({}, { onSale: true, price: 0 });
};

Product.fireSale().then(res => console.log(res));
```

### Mongoose Virtuals

  - Virtuals are document properties that you can get and set but that do not get persisted to MongoDB
  - **Getters** are useful for formatting or combining fields
  - **Setters** are useful for de-composing a single value into multiple values for storage.
  - Derived from the existing data

```js
const personSchema = new mongoose.Schema({
	first: String,
	last: String,
});

personSchema.virtual('fullName').get(function () {
	return `${this.first} ${this.last}`;
});

const Person = mongoose.model('Person', personSchema);
```

### Mongoose Middleware

  - https://mongoosejs.com/docs/middleware.html

  - pre/post hooks
  - To run code before and after certain things are executed
    - Ex. before something is removed or after something is saved
    - Ex. when deleting a user, deleting all associated comments, photos, etc.
      - Similar to FOREIGN KEY ON DELETE CASCADE from PSQL

```js
personSchema.pre('save', async function () {
  this.first = 'YO';
  this.last = 'OY';
  console.log('ABOUT TO SAVE')
})

personSchema.post('save', async function () {
  console.log('JUST SAVED')
})
```

#### Middleware for Deleting

  - For `findByIdAndDelete()`, it triggers `findOneAndDelete` middleware
    - https://mongoosejs.com/docs/api/model.html#model_Model.findByIdAndDelete
    - use query middleware (`findOneAndDelete`)

```js
// middleware for delete
// pre doesn't contain data
farmSchema.pre('findOneAndDelete', async function (data) {
  this.isModified('password')   // checks if the field 'password' has been modified
	console.log('Pre-middleware');
	console.log(data);
});

// post returns deleted data
farmSchema.post('findOneAndDelete', async function (farm) {
	if (farm.products.length) {
		// delete all the ids in products array
		const res = await Product.deleteMany({ _id: { $in: farm.products } });
		console.log(res);
	}
	console.log('Post-middleware');
});
```