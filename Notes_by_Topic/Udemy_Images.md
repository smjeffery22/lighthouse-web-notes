# Image Upload

  - Default HTHML form does not send file information
  
  - Need to change encoding type attribute on the form
    - Default value is `application/x-www-form-urlencoded`

  - `enctype="multipart/form-data"` included in the form element as an attribute

```html
<form action="/campgrounds" method="POST" novalidate class="validated-form" enctype="multipart/form-data">
  <input type="file" name="image" multiple>
</form>
```

## Multer
  - Need `Multer` Node.js middleware for handling multipart form-data
    - Primarily used for uploading files

  - `input` element with `file` type and `multiple` for uploading multiple files

```js
router.route('/')
	.post(upload.array('image'), (req, res) => {
		console.log(req.body, req.files)
		res.send('Uploaded')
	})
```
  - Multer adds a `body` object and `file/files` object to the `request` object

  - `upload.file('input_name')` for single file upload
    - `req.file`

  - `upload.array('input_name')` for multiple files upload
    - `req.files`

## Cloudinary

  - Cloud-based image and video management services
  - Allows users to upload, store, manage, manipulate and deliver images and video for websites and apps

## Multer Storage Cloudinary

  - Multer storage engine for Cloudinary

  - To upload files that Multer parses to Cloudinary
    - Get back URL from Cloudinary and Multer adds them in route handling callbacks

```js
const cloudinary = require('cloudinary').v2;
const { CloudinaryStorage } = require('multer-storage-cloudinary');

// cloudinary configuration
cloudinary.config({
	cloud_name: process.env.CLOUDINARY_CLOUD_NAME,
	api_key: process.env.CLOUDINARY_API_KEY,
	api_secret: process.env.CLOUDINARY_SECRET,
});

// storage in Cloudinary
const storage = new CloudinaryStorage({
	cloudinary,
	folder: 'YelpCamp',
	allowedFormats: ['jpeg', 'png', 'jpg'],
});

module.exports = {
	cloudinary,
	storage,
};
```