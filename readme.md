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
