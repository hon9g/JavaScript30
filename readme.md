![](https://javascript30.com/images/JS3-social-share.png)

# JavaScript30

Vanilla JavaScript 30 Day Challenge.
Grab the course at [https://JavaScript30.com](https://JavaScript30.com)

## Day1: Access to the DOM
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
<img src='https://user-images.githubusercontent.com/26381972/71594554-bff99c80-2b7b-11ea-9f47-8532a976a3a7.png' width='300'>

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
<img src='https://user-images.githubusercontent.com/26381972/71596588-3948bd80-2b83-11ea-9c75-a82eb593f1a0.png' width='300'>
<img src='https://user-images.githubusercontent.com/26381972/71596534-0f8f9680-2b83-11ea-9dac-af4c7281ef73.png' width='300'>

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
![image](https://user-images.githubusercontent.com/26381972/71644324-0d0b7900-2d0a-11ea-8b5c-811932573742.png)
![image](https://user-images.githubusercontent.com/26381972/71644785-a4c09580-2d11-11ea-96c6-9b09b8e6ff3a.png)
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