---
title:  "Check if a numeric key was pressed in JavaScript"
date:   2014-09-01 19:22:31
categories: javascript
---

If you ever need to see if a key is numeric in JavaScript (say for validation of fields that only allow numbers), check out the following example. In this case, we've also allowed for '.', 'delete' and 'backspace' to be pressed as well as cancelling the validation if modifiers such as alt and ctrl are pressed at the same time. The event that must be used if you want to cancel if the check fails is `keydown`, because if you use `keyup` then the key is already entered.

This sample relies on [underscore.js](http://underscorejs.org/) but could be easily changed to not require that library.

{% highlight javascript %}
function checkNumeric(e) {
    var isNumeric = (e.keyCode >= 48 && e.keyCode <= 57) || // Keyboard Numbers
                    (e.keyCode >= 96 && e.keyCode <= 105) // NUMPAD;

    var modifiers = (e.altKey || e.ctrlKey);

    var nonNumericAllowed = [46, 8, 110, 190]; // . delete backspace

    // Check to see if the key pressed was numeric, if not don't use it (except . and backspace and del)
    if (!isNumeric && !modifiers && !_.contains(nonNumericAllowed, e.keyCode)) {
        e.keyCode = 0;
        return false;
    }
}
{% endhighlight %}