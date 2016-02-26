# It's 2016; Things Have Changed

"You Don't Need jQuery" is based on [You Might Not Need jQuery](https://github.com/HubSpot/YouMightNotNeedjQuery), but is updated to reflect new APIs, new methodologies, and better, more simplified examples. 

**10 years after jQuery's initial release, the browser landscape has drastically changed.**

I'm not telling you to avoid using libraries, but I want you to be aware of the (new) native APIs that are available to you that, in some cases, are easier and more intuitive than those that jQuery (and others) have to offer.

---

[...] Please take a moment to consider if you actually need jQuery as a dependency; maybe you can include a few lines of utility code, and forgo the requirement. If you're only targeting more modern browsers, you might not need anything more than what the browser ships with.

[...] Some developers believe that jQuery is protecting us from a great demon of browser incompatibility when, in truth, [modern] browsers are pretty easy to deal with on their own.

**- YouMightNotNeedjQuery.com**

---

# Modern Browsers
Browsers today are nothing like their legacy counter-parts. The "big three"--being Chrome, Firefox, and Edge--are what we call, "evergreen", meaning that they self-regulate updates, giving you the most updated engines available. "**You Don't Need jQuery**" only focuses on these modern, evergreen browsers. If you need to support more legacy browsers, like IE, try reading [You Might Not Need jQuery](https://github.com/HubSpot/YouMightNotNeedjQuery) instead.

---
# You Don't Need jQuery

Most of the APIs that I'll be showing can be [polyfilled](https://en.wikipedia.org/wiki/Polyfill), meaning that you can recreate these features once, and then use all over your code.

---

## AJAX GET

**jQuery**
```javascript
$.ajax({
    url: 'path/to/json',
    success: data => {
        // ...
    },
    error: error => {
        // ...
    }
});
```

**Modern** | Using the [fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) and [Promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)
```javascript
fetch('/path/to/json')
.then(response => response.json())
.then(data => {
    // ...
})
.catch(error => {
    // ...
});
```

---

## AJAX POST

**jQuery**
```javascript
$.ajax({
    url: 'path/to/whatever',
    type: 'POST',
    contentType: 'application/json',
    data: JSON.stringify(myObjectHere),
    success: data => {
        // ...
    },
    error: error => {
        // ...
    }
});
```

**Modern** | Using the [fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) and [Promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)
```javascript
fetch('path/to/whatever', {
    method: 'POST',
    headers: new Headers({ 'Content-Type': 'application/json' }),
    body: JSON.stringify(myObjectHere)
})
.then(response => response.json())
.then(data => {
    // ...
})
.catch(error => {
    // ...
});
```

---

## Querying the DOM
via CSS selectors

**jQuery**
```javascript
const myElement = $('.foo');
```

**Modern** | Using [querySelector|All](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector)
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

**Modern** | Using the [classList API](https://developer.mozilla.org/en-US/docs/Web/API/Element/classList)
```javascript
myElement.classList.add('foo');
myElement.classList.remove('foo');
myElement.classList.toggle('foo');
```

---

## Getting/Setting Attributes

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

## Setting Text & HTML

**jQuery**
```javascript
$(myElement).text('lorem ispum');
$(myElement).html('<span>lorem ipsum</span>');
```

**Modern** | Using native properties
```javascript
myElement.textContent = 'lorem ipsum';
myElement.innerHTML = '<span>lorem ipsum</span>';
```

---

## Data Attributes

**jQuery**
```javascript
$(myElement).attr('data-foo', 'bar');
```

**Modern** | Using the [dataset API](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/dataset)
```javascript
myElement.dataset.foo = 'bar';
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

**Modern**
```javascript
myElement.appendChild(anotherElement);
myElement.insertBefore(anotherElement, myElement.firstChild);
myElement.remove();
```

---

## Event Listeners

**jQuery**
```javascript
$(myElement).on('click', e => { 
    // ... 
});
```

**Modern**
```javascript
myElement.addEventListener('click', e => { 
    // ... 
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
Array.from(myMultipleElements).filter(element => element.classList.contains('some-class-here'));
```

---

## Each Element

**jQuery**
```javascript
$(myMultipleElements).each((i, element) => {
    // ...
});
```

**Modern**
```javascript
Array.from(myMultipleElements).forEach((element, i) => {
    // ...
});
```

---

## Parent Element

**jQuery**
```javascript
const parent = $(myElement).parent();
```

**Modern**
```javascript
const parent = myElement.parentNode;
```

---

## Children

**jQuery**
```javascript
const children = $(myElement).children();
```

**Modern**
```javascript
const children = myElement.childNodes;
```

---

## Siblings

**jQuery**
```javascript
const siblings = $(myElement).siblings();
```

**Modern**
```javascript
const siblings = Array.from(myElement.parentNode.childNodes).filter(element => element !== myElement);
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
myElement.style.display = 'none';
myElement.style.display = null;
```

---

WIP
