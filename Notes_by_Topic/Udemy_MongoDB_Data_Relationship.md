# Data Relationship

## MongoDB Schema Design

  - https://www.mongodb.com/blog/post/6-rules-of-thumb-for-mongodb-schema-design-part-3

  - Start with embedding unless there is a compelling reason not to
    - If frequently needed to access certain object, reason not to embed
  
  - If arrays grow without bound, do not embed
    - If there are hundreds of documents on the "many side"
  
  - If there are thousands of documents on the "many side"
    - Include object id on the child side (i.e. "many side") referencing the parent
  
  

## One-to-Few

  - When there is a relatively small set of information to embed
  - Embed data under the parent document

  - Mongo adds an *id* for *each document*
  - An id will be created under addresses when a user model is created
    - Can be excluded by adding `_id: { id: false }` under schema definition
    - Mongoose treats each address object as an embedded schema

```js
const userSchema = new mongoose.Schema({
	first: String,
	last: String,
	addresses: [
		{
			_id: { id: false },
			street: String,
			city: String,
			province: String,
			country: String,
		},
	],
});

const User = mongoose.model('User', userSchema);

const makeUser = async () => {
	const u = new User({
		first: 'Jeffery',
		last: 'Park',
	});

	u.addresses.push({
		street: '123456 New St.',
		city: 'Toronto',
		province: 'ON',
		country: 'Canada',
	});

	const res = await u.save();
	console.log(res);
};
```

## One-to-Many

  - Store reference to the chile on the parent
  - Store the reference to the documents that are stored somewhere else
    - Using id

  - `type: Schema.Types.ObjectId` to include id
    - Populate (https://mongoosejs.com/docs/populate.html)
    - `ref` to tell Mongoose which model to use during population

  - When data from the Product model is inserted into products array:
    - Mongoose shows the product data was inserted into the array
    - Mongo shell shows only id
  
```js
const { Schema } = mongoose;

const farmSchema = new Schema({
	name: String,
	city: String,
	products: [
		{
			type: Schema.Types.ObjectId,  // mongoose.Schema.Types.ObjectId
			ref: 'Product',               // referencing model
		},
	],
});
```

### Mongoose Populate

  - `.populate('field_name')` to show the data, not only id

```js
Farm.findOne({ name: 'Full Belly Farms' })  // shows object ids only
	.populate('products')                     // shows whole data in products field
	.then((farm) => console.log(farm));

/*
 * // unpopulated
 * {
 *   _id: new ObjectId("6227d229deef25301fe24cbf"),
 *   name: 'Full Belly Farms',
 *   city: 'Niagara Falls, ON',
 *   products: [
 *     new ObjectId("6227ce976f113bb795d9912f"),
 *     new ObjectId("6227ce976f113bb795d99130")
 *   ],
 *   __v: 1
 * }
 * 
 * // populated
 * {
 *   _id: new ObjectId("6227d229deef25301fe24cbf"),
 *   name: 'Full Belly Farms',
 *   city: 'Niagara Falls, ON',
 *   products: [
 *     {
 *       _id: new ObjectId("6227ce976f113bb795d9912f"),
 *       name: 'Goddess Melon',
 *       price: 4.99,
 *       season: 'Summer',
 *       __v: 0
 *     },
 *     {
 *       _id: new ObjectId("6227ce976f113bb795d99130"),
 *       name: 'Sugar Baby Watermelon',
 *       price: 4.99,
 *       season: 'Summer',
 *       __v: 0
 *     }
 *   ],
 *   __v: 1
 * }
*/
```

## One-to-'Bajillions'

  - Store reference to the parent on the child
    - Insert object in child model
      - Shows only object id
      - Use populate() method to show all data
        - Second argument to populate specific values

```js
const userSchema = new Schema({
	username: String,
	age: Number,
});

const tweetSchema = new Schema({
	text: String,
	likes: Number,
	user: {
		type: Schema.Types.ObjectId,
		ref: 'User',
	},
});

const User = mongoose.model('User', userSchema);
const Tweet = mongoose.model('Tweet', tweetSchema);

// const makeTweets = async () => {
// 	// const user = new User({
// 	// 	username: 'chickenfan99',
// 	// 	age: 61,
// 	// });

// 	const tweet1 = new Tweet({
// 		text: 'I love chicken 99',
// 		likes: 0,
// 	});

// 	const user = await User.findOne({ username: 'chickenfan99' });
// 	const tweet2 = new Tweet({
// 		text: 'I hate chicken 9999',
// 		likes: 2,
// 	});

// 	tweet1.user = user; // insert the entire user object, but only saves user id
// 	tweet2.user = user; // insert the entire user object, but only saves user id

// 	// user.save();
// 	tweet1.save();
// };

// makeTweets();

const findTweet = async () => {
	// const t = await Tweet.findOne({}).populate('user', 'username');
	const t = await Tweet.find({}).populate('user', 'username');
	console.log(t);
};

findTweet();
```