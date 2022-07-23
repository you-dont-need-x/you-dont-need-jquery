# You Don't Need jQuery

"You Don't Need jQuery" is based on [You Might Not Need jQuery](https://github.com/HubSpot/YouMightNotNeedjQuery), but is updated to reflect new APIs, new methodologies, and better, more simplified examples. 

### It's 2018; Things Have Changed

**10+ years after jQuery's initial release, the browser landscape has drastically changed.**

The purpose of this is not to tell you that you shouldn't use jQuery, but rather to re-educate you on what exactly jQuery is useful for. The DOM, and other browser APIs, have been much better standardized, and many of the previous pitfalls of compatibility no longer exist. While jQuery is still useful, it is less so than before, and it's important for you--the developer--to be familiar with the underlying APIs that libraries are abstracting.

A lot of the new APIs and methodologies are much easier to understand, and are sometimes more coherent than those in libraries like jQuery.

---

*[...]* Please take a moment to consider if you actually need jQuery as a dependency; maybe you can include a few lines of utility code, and forgo the requirement. If you're only targeting more modern browsers, you might not need anything more than what the browser ships with.

*[...]* Some developers believe that jQuery is protecting us from a great demon of browser incompatibility when, in truth, *[modern]* browsers are pretty easy to deal with on their own.

**- YouMightNotNeedjQuery.com**

---

Most of the APIs that I'll be showing can be [polyfilled](https://en.wikipedia.org/wiki/Polyfill_(programming)), meaning that if the browser is modern, and supports the APIs, it will use those, but if the browser is legacy, it will update the APIs with the new features, and allow all browsers to work.

**Modern features that can be polyfilled for legacy browsers:**
- Promise
- fetch
- classList
- Array.from
- Object.assign
- More...

Although a couple of the modern examples have more characters in their code, they should not deter you from trying to understand these new APIs. Read carefully, and try to understand what the code is doing so that you can better reflect on whether or not you should use a library.

---

## AJAX GET

**jQuery**
```javascript
$.ajax({
    url: '/path/to/json',
    success: data => {
        // use 'data' here
    },
    error: error => {
        // use 'error' here
    }
});
```

**Modern** | Using the [fetch API](https://devdocs.io/dom/fetch_api/using_fetch) and [Promises](https://devdocs.io/javascript/global_objects/promise)
```javascript
fetch('/path/to/json')
.then(response => response.json())
.then(data => {
    // use 'data' here
})
.catch(error => {
    // use 'error' here
});
```

**New** | Using [async/await](https://devdocs.io/javascript/statements/async_function)
```javascript
try {
    const response = await fetch('/path/to/json');
    const data = await response.json();
    // use 'data' here
}
catch (error) {
    // use 'error' here
}
```

---

## AJAX POST

**jQuery**
```javascript
$.ajax({
    url: '/path/to/whatever',
    type: 'POST',
    contentType: 'application/json',
    data: JSON.stringify(myObjectHere),
    success: data => {
        // use 'data' here
    },
    error: error => {
        // use 'error' here
    }
});
```

**Modern** | Using the [fetch API](https://devdocs.io/dom/fetch_api/using_fetch) and [Promises](https://devdocs.io/javascript/global_objects/promise)
```javascript
fetch('/path/to/whatever', {
    method: 'POST',
    headers: { 'content-type': 'application/json' },
    body: JSON.stringify(myObjectHere)
})
.then(response => response.json())
.then(data => {
    // use 'data' here
})
.catch(error => {
    // use 'error' here
});
```

**New** | Using [async/await](https://devdocs.io/javascript/statements/async_function)
```javascript
try {
    const response = await fetch('/path/to/whatever', {
        method: 'POST',
        headers: { 'content-type': 'application/json' },
        body: JSON.stringify(myObjectHere)
    });
    const data = await response.json();
    // use 'data' here
}
catch (error) {
    // use 'error' here
}
```

---

## Querying the DOM
via CSS selectors

**jQuery**
```javascript
const myElement = $('.foo');
```

**Modern** | Using [querySelector](https://devdocs.io/dom/element/queryselector) or [querySelectorAll](https://devdocs.io/dom/element/queryselectorall)
```javascript
const myElement = document.querySelector('.foo');
// or
const myMultipleElements = document.querySelectorAll('.foo');
```

---

## Element's Class
add | remove | toggle

**jQuery**
```javascript
$(myElement).addClass('foo');
$(myElement).removeClass('foo');
$(myElement).toggleClass('foo');
```

**Modern** | Using the [classList API](https://devdocs.io/dom/element/classlist)
```javascript
myElement.classList.add('foo');
myElement.classList.remove('foo');
myElement.classList.toggle('foo');
```

---

## Attributes
get | set

**jQuery**
```javascript
const foo = $(myElement).attr('foo');
$(myElement).attr('bar', foo);
```

**Modern**
```javascript
const foo = myElement.getAttribute('foo');
myElement.setAttribute('bar', foo);
```

---

## Input's Value
get | set

**jQuery**
```javascript
const value = $(myElement).val();
$(myElement).val('foo');
```

**Modern**
```javascript
const value = myElement.value;
myElement.value = 'foo';
```

---

## Text & HTML

**jQuery**
```javascript
$(myElement).text('lorem ispum');
$(myElement).html('<span>lorem ipsum</span>');
$(myElement).append('<span>foo bar</span>');
```

**Modern** | Using native properties and [insertAdjacentHTML](https://devdocs.io/dom/element/insertadjacenthtml)
```javascript
myElement.textContent = 'lorem ipsum';
myElement.innerHTML = '<span>lorem ipsum</span>';
myElement.insertAdjacentHTML('beforeend', '<span>foo bar</span>');
```

---

## Data Attributes

**jQuery**
```javascript
$(myElement).data('foo', 'bar');
```

**Modern** | Using the [dataset API](https://devdocs.io/dom/htmlelement/dataset)
```javascript
myElement.dataset.foo = 'bar';
```

---

## Element Styles

**jQuery**
```javascript
$(myElement).css({ background: 'red', color: 'white' });
```

**Modern**
```javascript
Object.assign(myElement.style, { background: 'red', color: 'white' });
// or
myElement.style.background = 'red';
myElement.style.color = 'white';
```

---

## Append Child & Remove Element
append | prepend | remove

**jQuery**
```javascript
$(myElement).append(anotherElement);
$(myElement).prepend(anotherElement);
$(myElement).remove();
```

**Modern** | Using [remove](https://devdocs.io/dom/childnode/remove)
```javascript
myElement.appendChild(anotherElement);
myElement.insertBefore(anotherElement, myElement.firstChild);
myElement.remove();
```

**New** | Using [append](https://devdocs.io/dom/parentnode/append) and [prepend](https://devdocs.io/dom/parentnode/prepend) as well
```javascript
myElement.append(anotherElement);
myElement.prepend(anotherElement);
myElement.remove();
```

---

## Event Listeners
add | remove

**jQuery**
```javascript
$(myElement).on('click', myEventHandler);
$(myElement).off('click', myEventHandler);
```

**Modern** | Using [addEventListener](https://devdocs.io/dom/eventtarget/addeventlistener) and [removeEventListener](https://devdocs.io/dom/eventtarget/removeeventlistener)
```javascript
myElement.addEventListener('click', myEventHandler);
myElement.removeEventListener('click', myEventHandler);
```

---

## Delegated Events

**jQuery**
```javascript
$(myRootElement).on('click', myTargetElements, myEventHandler);
```

**Modern** | Using [composedPath](https://developer.mozilla.org/en-US/docs/Web/API/Event/composedPath) and [matches](https://developer.mozilla.org/en-US/docs/Web/API/Element/matches)
```javascript
myRootElement.addEventListener('click', (event, ...args) {
  const matches = event.composedPath()
    .filter( (el) => el instanceof HTMLElement )
    .find( (el) => el.matches( myTargetElements ) );
  if (matches) 
    eventHandler.call(event.currentTarget, event, matches, ...args);
});
```

---

## Filter Elements

**jQuery**
```javascript
$(myMultipleElements).filter('.some-class-here');
```

**Modern**
```javascript
Array.from(myMultipleElements).filter(x => x.classList.contains('some-class-here'));
```

---

## Find Elements
from single | from multiple

**jQuery**
```javascript
const x = $(myElement).find('.foo');
const y = $(myMultipleElements).find('.foo');
```

**Modern** | (This one is probably not a great example...)
```javascript
const x = myElement.querySelectorAll('.foo');
const y = Array.from(myMultipleElements, x => Array.from(x.querySelectorAll('.foo'))).reduce((a, b) => a.concat(b));
```

**New** | Using [flat](https://devdocs.io/javascript/global_objects/array/flat)
```javascript
const x = myElement.querySelectorAll('.foo');
const y = Array.from(myMultipleElements, x => Array.from(x.querySelectorAll('.foo'))).flat();
```

---

## Each Element

**jQuery**
```javascript
$(myMultipleElements).each((i, x) => {
    // use 'x' here
});
```

**Modern**
```javascript
Array.from(myMultipleElements).forEach((x, i) => {
    // use 'x' here
});
```

**New** | Using [for..of](https://devdocs.io/javascript/statements/for...of) and [entries](https://devdocs.io/javascript/global_objects/array/entries)
```javascript
for (const [i, x] of Array.from(myMultipleElements).entries()) {
    // use 'x' here
}
```

---

## Parent Element

**jQuery**
```javascript
const parent = $(myElement).parent();
```

**Modern**
```javascript
const parent = myElement.parentElement;
```

---

## All Parents

**jQuery**
```javascript
const parents = $(myMultipleElements).parents('.foo');
```

**Modern** | Using [closest](https://devdocs.io/dom/element/closest)
```javascript
const parents = Array.from(myMultipleElements, x => x.closest('.foo'));
```

---

## Children

**jQuery**
```javascript
const children = $(myElement).children();
```

**Modern**
```javascript
const children = myElement.children;
```

---

## Siblings

**jQuery**
```javascript
const siblings = $(myElement).siblings();
```

**Modern**
```javascript
const siblings = Array.from(myElement.parentNode.children).filter(x => x !== myElement);
```

---

## Next & Previous Sibling

**jQuery**
```javascript
const next = $(myElement).next();
const prev = $(myElement).prev();
```

**Modern**
```javascript
const next = myElement.nextElementSibling;
const prev = myElement.previousElementSibling;
```

---

## Hide & Show Element

**jQuery**
```javascript
$(myElement).hide();
$(myElement).show();
```

**Modern**
```javascript
myElement.hidden = true;
myElement.hidden = false;
```

---

**This repo of knowledge is a work in progress; if you'd like to contribute, please submit an issue or a pull request.**
