![](https://javascript30.com/images/JS3-social-share.png)

# JavaScript30

Vanilla JavaScript 30 Day Challenge.
Grab the course at [https://JavaScript30.com](https://JavaScript30.com)

## Day1: Access to the DOM
![image](https://user-images.githubusercontent.com/26381972/71702379-7f678080-2e12-11ea-8c7d-7971a3199c2c.png)
#### 1. To access to the DOM element
- `Document.querySelector()`
  - Returns the first Element node within the document, in document order, that matches the specified selectors.
- `Document.querySelectorAll()`
  - Returns a list of all the Element nodes within the document that match the specified selectors.
#### 2. To add event
: The EventListener interface represents an object that can handle an event dispatched by an EventTarget object.
- `EventTarget.addEventListener(type, listener)`
  - `type`: a keyword that represent event type to listen for.
  - `listener`: EventListener interface || JS function
- `window.addEventListener('keydown', playSound)`
  - if `keydown` event occurs play a listener `playSound`

## Day2: Update styles every second
![image](https://user-images.githubusercontent.com/26381972/71702821-d8381880-2e14-11ea-90bc-8c4fe3e3a59f.png)
#### 1. Access and update styles of element nodes
`node.style.property = value`
```JavaScript
const now = new Date();
const s = now.getSeconds();
const m = now.getMinutes();
const h = now.getHours();

secondHand.style.transform = `rotate(${(s / 60) * 360 + 90}deg)`;
minHand.style.transform = `rotate(${(m / 60) * 360 + 90}deg)`;
hourHand.style.transform = `rotate(${(h / 12) * 360 + 90}deg)`;
```

## Day3: CSS Variables
![image](https://user-images.githubusercontent.com/26381972/71702171-3d8a0a80-2e11-11ea-8c21-908c2093981b.png)

#### 1. css custom properties
Property names that are prefixed with `--` represent custom properties that contain a value
```CSS
:root {
  --base: #ffc600;
  --spacing: 10px;
  --blur: 10px;
}
```
#### 2. css variables
custom properties can be used in other declarations using the `var()` function.
```CSS
img {
  padding: var(--spacing);
  background: var(--base);
  filter: blur(var(--blur));
}
```
#### 3. update css property
```
style.setProperty(propertyName, newValue);
```
```JavaScript
const inputs = document.querySelectorAll('.controls input')
function handleUpdate() {
  const suffix = this.dataset.sizing || '';
  document.documentElement.style.setProperty(
    `--${this.name}`, this.value + suffix
    );
}
inputs.forEach(e => e.addEventListener('change', handleUpdate));
inputs.forEach(e => e.addEventListener('mousemove', handleUpdate));
```

## Day 4: Array Methods
#### `array.filter(callback)`
- The `filter()` method creates a new array with all elements that pass the callback function.
```JavaScript
// 1. Filter the list of inventors for those who were born in the 1500's
const fifteens = inventors.filter(e => 1500 <= e.year && e.year < 1600 );
```
#### ` array.map(callback)`
- The `map()` method creates a new array populated with the results of the callback function on every element.
```JavaScript
// 2. Give us an array of the inventors' first and last names
const fullNames = inventors.map( e => `${e.first} ${e.last}`);
```
#### `array.sort([compareFunction])`
- The `sort()` method sorts the elements of an array in place and returns the sorted array.
```JavaScript
// 3. Sort the inventors by birthdate, oldest to youngest
const oldToYoung = inventors.sort((a, b) => a.year - b.year);

// 7. Sort the people alphabetically by last name
const orderedPeople = people.sort((a, b) => {
  const [firstA, lastA] = a.split(', ');
  const [firstB, lastB] = b.split(', ');
  return lastA > lastB ? 1 : -1;
});
```
#### `arr.reduce(callback[, initialValue])`
- The `reduce()` method executes a reducer function on each element of the array, resulting in single output value.
```JavaScript
// 4. How many years did all the inventors live?
const totalYear = inventors.reduce((years, e) => years + e.passed - e.year, 0);

// 8. Sum up the instances of each of these
const data = ['car', 'car', 'truck', 'truck', 'bike', 'walk', 'car', 'van', 'bike', 'walk', 'car', 'van', 'car', 'truck' ];
const countData = data.reduce((count, key) => {
  if (!count[key]) {
    count[key] = 0;
  }
  count[key]++;
  return count;
}, {});
```

## Day 5: flexible layout
![image](https://user-images.githubusercontent.com/26381972/71702092-d704ec80-2e10-11ea-9fa3-d088feacdd03.png)
The flex layout aims at providing a more efficient way to align and distribute space among items in a container, even when their size is unknown and/or dynamic. _(a W3C Candidate Recommendation as of October 2017)_
#### flex items in same ratio
```HTML
<div class="container">
  <div class="item"></div>
  <div class="item"></div>
  <div class="item"></div>
</div>
```
```CSS
.container {
  display: flex;
}
.item {
  flex: 1;
}
```
#### more properties for a Flex Container
| property | value |
|:---:|:---:|
`display` | defines a flex container.
`flex-direction` | establishes the main-axis of flex items.
`flex-wrap` | sets how to wrap flex items. `nowrap (default)` \| `wrap` \|  `wrap-reverse`
`flex-flow` | is shortcut of `flex-direction` and `flex-wrap`.
`justify-content` | defines the alignment along the main axis.
`align-content` | defines the alignment along cross axis. (more than 2 line)
`align-items` | defines the alignment along cross axis. (1 line)

#### more properties for Flex Item
| property | value |
|:---:|:---:|
`order` | controls the order of flex item in the flex container.
`flex` | is a shortcut of `flex-grow`, `flex-shrink`, `flex-basis`
`flex-grow` | defines the ability for a flex item to grow if necessary.
`flex-shrink` | defines the ability for a flex item to shrink if necessary.
`flex-basis` | defines the default size of a flex item before the remaining space is distributed.
`align-self` | defines the alignment of Item along a cross axis.

- reference
  - [A Complete Guide to Flexbox (EN)](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
  - [CSS Flex(Flexible Box) 완벽 가이드 (KR)](https://heropy.blog/2018/11/24/css-flexible-box/)

## Day 6: Typeahead
![image](https://user-images.githubusercontent.com/26381972/71693228-42d65d80-2def-11ea-895d-1cec75fa5ff1.png)

#### Fetching Data
- [`fetch(resource[, init])`](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/fetch)
- The `fetch()` method starts the process of fetching a resource from the network, returning a promise which is fulfilled once the response is available.
```JavaScript
const cities = [];
const endpoint = 'https://gist.githubusercontent.com/Miserlou/c5cd8364bf9b2420bb29/raw/2bf258763cdddd704f8ffd3ea9a3e81d25e2c6f6/cities.json';

fetch(endpoint)
  .then(blob => blob.json())
  .then(data => cities.push(...data));
```

#### Regular Expression in JS
##### [`new RegExp(pattern[, flags])`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp)
- The `RegExp` constructor creates a regular expression object for matching text with a pattern.
- `flags`
  - `g`: global match; find all matches rather than stopping after the first match.
  - `i`: ignore case; if u flag is also enabled, use Unicode case folding.
  - `m`: multiline; treat beginning and end characters (^ and $) as working over multiple lines.
  - `s`: "dotAll"; allows . to match newlines.
  - `u`: Unicode; treat pattern as a sequence of Unicode code points. (See also Binary strings).
  - `y`: sticky; matches only from the index indicated by the lastIndex property of this regular expression in the target string (and does not attempt to match from any later indexes).
```JavaScript
const findMatches = (wordToMatch, cities) => {
  const regex = new RegExp(wordToMatch, 'gi');
  return cities.filter(e => e.city.match(regex) || e.state.match(regex));
}
```

- To create a regular expression can calling the constructor function of the `RegExp` object, as above.
- Using the constructor function provides runtime compilation of the regular expression.
- Use the constructor function when you know the regular expression pattern will be changing, or you don't know the pattern and are getting it from another source, such as user input.

##### [`/pattern/modifiers;`](https://www.w3schools.com/jsref/jsref_obj_regexp.asp)
- To create a regular expression can using literal, which consists of a pattern enclosed between slashes.
- Regular expression literals provide compilation of the regular expression when the script is loaded.
- If the regular expression remains constant, using this can improve performance.

```JavaScript
const numberWithCommas = x => x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, '.');

function displayMatches() {
  const regex = new RegExp(this.value, 'gi');
  const matched = findMatches(this.value, cities);
  const html = matched.map(e => {
    const cityName = e.city.replace(regex, `<span class='hl'>${this.value}</span>`);
    const stateName = e.state.replace(regex, `<span class='hl'>${this.value}</span>`);
    return `
      <li>
        <span class='name'>${cityName}, ${stateName}</span>
        <span class='population'>${numberWithCommas(e.population)}</span>
      </li>
    `;
  }).join('');
  suggestions.innerHTML = html;
}
```
| Metacharacter | role |
|:---:|:---:|
|`\B`|to find a match which is not present at the beginning or end of a word. If a match is found it returns the word else it returns NULL.
|`\d`|to search digit characters. It is same as `[0-9]`.

| Quantifier | role |
|:---:|:---:|
|`p+`| to find match any string containing one or more p.
|`?=p`|to find match any string which is followed by a specific p.
|`?!p`|to find the match of any string which is not followed by a specific p.
|`p{N}`| to find match any string containing a sequence of N times p.

- reference
  - [MDN - Regular_Expressions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions)
  - [W3S - RegExp Literal grammar](https://www.w3schools.com/jsref/jsref_obj_regexp.asp)
  - [tp - RegExp Literal grammar](https://www.tutorialspoint.com/javascript/javascript_regexp_object.htm)

## Day 7: Array Methods 2
#### [`array.some(callback[, thisArg])`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/some)
- tests whether at least one element in the array passes the provided callback function.
- returns a Boolean value.
```JavaScript
// is at least one person 19 or older?
const currentYear = new Date().getFullYear();
const oneAdult = `
  ${people.some(e => e.year >= currentYear - 19)
    ? 'At least one person'
    : 'No one'
  } over 19.
`;
```
#### [`array.every(callback[, thisArg])`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/every)
- tests whether all elements in the array pass the provided callback function.
- returns a Boolean value.
```JavaScript
// is everyone 19 or older?
const allAdult = `
  ${people.every(e => e.year >= currentYear - 19)
    ? 'All'
    : 'Not all'
  } people are over 19.
`;
```
#### [`array.find(callback[, thisArg])`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find)
-  returns the value of the first element in the provided array that satisfies the provided callback function.
```JavaScript
// find the comment with the ID of 823423
const comment = comments.find(e => e.id === 823423);
```
#### [`array.findIndex(callback[, thisArg])`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex)
- returns the index of the first element in the array that satisfies the provided callback function.
- if no element passed the test, it returns -1.
```JavaScript
// find the index with the ID of 823423
const idx = comments.findIndex(e => e.id === 823423);
```
#### [`array.slice([begin[, end]])`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)
- returns a shallow copy of a portion of an array into a new array object selected from begin to end - 1.
```JavaScript
// create new array without a comment at comments[idx]
const newComments = [
  ...comments.slice(0, idx),
  ...comments.slice(idx+1)
];
```
#### [`array.splice(start[, deleteCount, item1, item2, ...])`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)
- changes the contents of an array by removing or replacing existing elements and/or adding new elements in place.
  - `start`: The index at which to start changing the array.
  - `deleteCount`: The number of elements to remove.
  - `item`: The elements to add to the array.
```JavaScript
// delete a comment at comments[idx]
comments.splice(idx, 1);
```
