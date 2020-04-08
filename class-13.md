### Notes from the following reading:
“The Past, Present, and Future of Local Storage for Web Applications”

@ http://diveinto.html5doctor.com/storage.html

___

HTML5 STORAGE SUPPORT

    IE | 8.0+
    FIREFOX | 3.5+
    SAFARI | 4.0+				
    CHROME | 4.0+
    OPERA | 10.5+
    IPHONE | 2.0+
    ANDROID | 2.0+

check for HTML5 Storage:

    function supports_html5_storage() {
      try {
        return 'localStorage' in window && window['localStorage'] !== null;
      } catch (e) {
        return false;
      }
    }

Using Modernizr to detect support for HTML5 Storage:

    if (Modernizr.localstorage) {
      // window.localStorage is available!
    } else {
      // no native support for HTML5 storage :(
      // maybe try dojox.storage or a third-party solution
    }

HTML5 Storage:
Notes:

The named key is a string. The data can be any type supported by JavaScript, including strings, Booleans, integers, or floats. However, the data is actually stored as a string. If you are storing and retrieving anything other than strings, you will need to use functions like parseInt() or parseFloat() to coerce your retrieved data into the expected JavaScript datatype.

    interface Storage {
      getter any getItem(in DOMString key);
      setter creator void setItem(in DOMString key, in any data);
    };

Calling setItem() +  Calling getItem()

-treat the localStorage object as an associative array

    var foo = localStorage.getItem("bar");
    // ...
    localStorage.setItem("bar", foo);

Could be rewritten to use square bracket syntax instead like below:

    var foo = localStorage["bar"];
    // ...
    localStorage["bar"] = foo;

For removing the value for a given named key:

    interface Storage {
     deleter void removeItem(in DOMString key);
     void clear();
    };

* This property gets the total number of values in the storage area, and to iterate through all of the keys by index (to get the name of each key).

    interface Storage {
      readonly attribute unsigned long length;
      getter DOMString key(in unsigned long index);
    };

note: If you call key() with an index that is not between 0–(length-1), the function will return null.

The storage event:

    if (window.addEventListener) {
      window.addEventListener("storage", handle_storage, false);
    } else {
      window.attachEvent("onstorage", handle_storage);
    };

note: The handle_storage callback function will be called with a StorageEvent object, except in Internet Explorer where the event object is stored in window.event.

    function handle_storage(e) {
      if (!e) { e = window.event; }
    }

note:

see HTML5 storage in action for further code examlpes.
___