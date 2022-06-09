# HTML

```js
<img src="" alt="">
```
  * Include 'alt' attribute for displaying in case image fails to load

```js
<p>Click here to view more <a href="https://catphotos.com" target="_blank">cat photos</a>.</p>
```
  * Anchor tag to include a text with link
  * Target="_blank" to open the link in a new tab

```js
<a href="#"><img src="https://fcc.im/fcc-relaxing-cat" alt="A cute ornage cat lying on its back."></a>`
```
  * Wrap img tag with anchor tag to make image a clickable link


```js
<form action="/submit-cat-photo">
  <label for="indoor"><input id="indoor" type="radio" name="indoor-outdoor" checked> indoor</label><br>
  <label for="outdoor"><input id="outdoor" type="radio" name="indoor-outdoor"> outdoor</label><br>

  <label for="loving"><input id="loving" type="checkbox" name="personality" checked>Loving</label><br>
  <label for="lazy"><input id="lazy" type="checkbox" name="personality">lazy</label><br>
  <label for="energetic"><input id="energetic" type="checkbox" name="personality">Energetic</label><br>

  <input type="text" placeholder="cat photo URL" required><br>
  <button type="submit">Submit</button>
</form>
```
  * 'required' attribute the form to be required to be filled
  * type="ratio" creates selectable circle buttons
    * Adding label tags allows the button to be clicked even if the text is clicked
    * Assigning name="indoor-outdoor" to the two buttons does not allow the buttons to be clicked at the same time
  * Assign for attribute to the label tag that matches the id of the input
    * To know the label is for that input
  * type="checkbox" creates checkbox
  * Adding 'checked' attritube after the 'name' attribute automatically checks off the field


