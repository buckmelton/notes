Buck's Javascript Notes

Data Types
  There are 6 data types in Javascript:
    - Number
      NaN (Not a Number) is a special kind of Number
    - String
    - Boolean
    - Null
    - Undefined
    - Object
      Arrays and Functions are of type Object

Truthy and Falsy
  Some things are treated _as_if_ they are false or true.

  Falsy:
    false (the traditional Boolean false)
    0 (the number 0)
    '' (empty string)
    10/'score' (NaN - Not a Number)
    var highScore; (a variable with no value assigned to it)

  Almost everything else is truthy:

  Truthy:
    true (Boolean true)
    1 (numbers other than 0)
    'carrot' (strings with content)
    10/5 (number calculations)
    'true' (true written as a string)
    '0' (zero written as a string)
    'false' (false written as a string)
    The presence of an object or an array

  Truthy values can also be treated as the number 1.

  IMPORTANT NOTE:
    if (document.getElementById('header') {
      // Found: do something
    } else {
      // Not found: do something else
    }

    is NOT the same as:

    if (document.getElementById('header') == true) {
      ...

    In the first case, it is truthy and _treated_as_if_ it were truth, and so "Found: do something" is executed.
    But it is not EQUAL TO true, so in the second case, "Not found: do something" is executed.

Conditionals:

  if (expr) {
  
  } else {

  }

  
  switch
