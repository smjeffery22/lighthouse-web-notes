# D3.js (DATA-DRIVEN DOCUMENTS)

  - Open source JS library
  - Create dynamic, interactive data visualizations in web browsers
    - Uses HTML, CSS and SVG
    - Can create DOM elements using data
  - https://www.freecodecamp.org/news/d3js-tutorial-data-visualization-for-beginners/

## SELECTION AND MANIPULATION

  - Include script tag in html file

  ```html
  <script src="https://d3js.org/d3.v7.min.js"></script>
  ```

  - Using D3,can select DOM elements using:
    - CSS selectors
    - Name of element itself
  
  - Two methods to select DOM elements
    1. `d3.select('h1')`
        - Selects the first element that matches in the DOM
    2. `d3.selectAll()`

  - Add style: `h1.style('color', 'red')`
  
  - Add attribute: `h1.attr('class', 'heading')`

  - Change text: `h1.text('Updated Heading')`

  - Append: `d3.select('body').append('p').text('First paragraph')`

### DYNAMIC PROPERTIES

  - Each DOM manipulation method takes in a constant value or a function as a parameter
    - Function takes in two properties:
      1. `d` data
      2. `i` index

## DATA JOIN

  ```html
  <div class="d3_fruit"></div>
  ```

  ```js
  const fruits = ['Apple', 'Orange', 'Mango'];

  d3.selectAll('.d3_fruit')
      .selectAll('p')
      .data(fruits)
      .join('p')
        .attr('class', 'd3_fruit')
        .text((d) => d);
  ```

  1. Select .d3_fruit div
  2. Select all p elements (empty selection)
  3. Binds the fruits array to the empty selection
  4. Creates all the p elements for each item in the array
  5. Sets class for each p element created
  6. Sets text for each p based on the array

## DATA LOADING

  - D3 has methods to load various types of files:
    - d3.json
    - d3.csv
    - d3.xml
    - d3.tsv
    - d3.text

  ```js
  // async await
  const data = await d3.csv("/path/to/file.csv");
  console.log(data);

  // or
  d3.json("/path/to/file.json").then((data) => {  console.log(data); })
  ```

## SCALES IN D3

  - `d3.scale` function takes in data as input and returns a visual value in pixels
    - Needs to be set with a *domain* and *range*
    - *domain* sets a LIMIT for the data
  
  - Various form of scales: https://github.com/d3/d3-scale

  ```js
  const x_scale = d3.scaleLinear()
    .domain([10, 500])
    .range([2000000, 16000000]);
  ```

  - `d3.scaleLinear():` tell D3 to use the scaleLinear
  - `.domain([10, 500]):` set the domain (Limit) from 10 to 500
  - `.range([2000000, 16000000]):` set min value to 2M and max value to 16M
    - map out '2M to 10px' and '16M to 500px'
      - for 8M, 250px
  




  - Using D3, can map data into DOM elements
    - Append, update or display DOM elements using data set
  
  ```js
  const dataset = [1, 2, 3, 4, 5];

  d3.select('body')
    .selectAll('p') // initially empty
    .data(dataset) // puts data into waiting state for further processing
    .enter() // take items one by one and perform further action
    .append('p') // appends paragraph tag for each data element
    // .text('D3 is awesome!') // displays the text with <p> tag5 times
    .text(function(d) { return d; }); // displayed 1, 2, 3, 4, 5 with <p> tags
  ```

## CREATING A SIMPLE BAR CHART

  - SVG tag in html file