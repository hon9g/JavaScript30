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
