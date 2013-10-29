---
layout: post
title: Android - Using TextWatcher to mask a numeric field
---

I recently created an android app to interface with [ketofinder.com](http://ketofinder.com), and it was a great learning experience. I wanted to share an interesting problem I had to solve regarding a TextWatcher object. 
[TextWatcher](http://developer.android.com/reference/android/text/TextWatcher.html) is an [interface](http://en.wikipedia.org/wiki/Interface_(Java)) in the android framework for listening to changes to an object that implements [Editable](http://developer.android.com/reference/android/text/Editable.html). 
For the ketofinder app I used a few TextWatcher objects to ensure that some numeric input fields would only accept numeric inputs from the user.

### NumericTextWatcher.java

<script src="https://gist.github.com/z3roshot/d43ce759a27904e4ca29.js"></script>

This class uses regular expressions see if the input value is only numeric, and if not it strips the non numeric characters. I wasn't interested in the beforeTextChanged method because I didn't need to do anything at that point. From the name, it seems like onTextChanged could be a good candidate for performing the check and edit, but according to the documentation for TextWatcher, "It is an error to attempt to make changes to s from this callback." So afterTextChanged was the appropriate candidate for what I needed to do.

### Net Carbs

As you can see in the following screen shot, there is a "Net Carbs" field:

<img style="-webkit-user-select: none" src="https://lh6.ggpht.com/JKF1OBPZwxH9b0EthSTgOIcJkb6Kfo3EPhKp6Fp67BOVeETl7bagyDfC1I09KHAxsGQ7=h900-rw">

The Net Carbs was a calculated value: Carbs - Fiber = Net Carbs. When a user enters numbers into Carbs or Fiber it recalculates the Net Carbs field. Here is the code for the calculation (We'll get to the catch block in a moment):

<script src="https://gist.github.com/z3roshot/35b364e8bfa33afb361a.js"></script>

This snippet is in a try - catch block because Integer.parseInt(...) can fail if any of the characters in the string are non numeric.

### Handle errors

Here is the code with the catch block filled in:

<script src="https://gist.github.com/z3roshot/05c9086102404f7f0f0d.js"></script>

You'll probably notice that I'm removing and adding the TextWatcher object from the Carbs and Fiber fields. If I didn't remove and re-add the watchers, editing the field would trigger the afterTextChanged method would fire again which would cause it to call updateNetCarbs() again and that would cause a call stack explosion into a stack overflow. The fix was to simply stop listening while I edit the field.

### In conclusion

TextWatcher is a fantastic tool for handling user input into an Editable object, such as EditText, but it has its pitfalls.