Buck's Javascript Notes

# Conventions
Filenames: dashes e.g. this-is-my-source-code.js
Variable names: camel case e.g. var myAwesomeVar = 0;

# Environment
## Outputting to Console
```javascript
console.log('Whatever is here gets written to console with a newline appended.');
process.stdout.write('Whatever is here gets written to console withOUT a newline appended.');
```

# Data Types
There are 6 data types in Javascript:
    - Number
      NaN (Not a Number) is a special kind of Number
    - String
    - Boolean
    - Null
    - Undefined
    - Object
      Arrays and Functions are of type Object

## Type Coercion and Weak Typing
JavaScript has weak typing and can convert data types behind the scenes to complete an operation.  
If you use a data type that JavaScript did not expect, it tries to make sense of the operation rather than report an error.

## === and !==
When checking if two values are equal or not equal, because of automatic type conversion it is considered better to use strict equals operators === and !== as those will check that values and data types match, while == and != only check that values match.

## Truthy and Falsy
Some things are treated _as_if_ they are false or true.

Falsy:
- false (the traditional Boolean false)
- 0 (the number 0)
- '' (empty string)
- 10/'score' (NaN - Not a Number)
- var highScore; (a variable with no value assigned to it)

Almost everything else is truthy:

Truthy:
- true (Boolean true)
- 1 (numbers other than 0)
- 'carrot' (strings with content)
- 10/5 (number calculations)
- 'true' (true written as a string)
- '0' (zero written as a string)
- 'false' (false written as a string)
- The presence of an object or an array

Truthy values can also be treated as the number 1.

IMPORTANT NOTE:
```javascript
if (document.getElementById('header')) {
  // Found: do something
} else {
  // Not found: do something else
}
```

is NOT the same as:
```javascript
if (document.getElementById('header') == true) {
      ...
```

In the first case, it is truthy and _treated_as_if_ it were truth, and so "Found: do something" is executed.  
But it is not EQUAL TO true, so in the second case, "Not found: do something" is executed.
    

## Short Cicuit Values:

Logical operators are processed left to right.  They short-circuit (stop) as soon as they have a result - but they return the value that stopped the processing (not necessarily true or false).
```javascript
var artist = 'Rembrandt';
var artistA = (artist || 'Unknown');
```

artistA ends up with value 'Rembrandt' because processing stops at truthy 'Rembrandt'

Therefore, in logical operations, put the code most likely to return true first in OR operations or the code most likely to return false in AND operations, or the code requiring the most processing power last, just in case another preceding value stops the operation earlier and the processor-intensive operation doesn't need to be run.
  
# Operators:

++  // increment  
--  // decrement


# Variables:

Variables declared without 'var' are considered _global_ variables, so don't accidently forget the 'var' in the declaration or it may very well cause unintended bugs and scope grief.

## Hoisting
Variables can be used before they are declared. _Hoisting_ means that javascript moves any declarations to the top.

Note that hoisting is only for declarations, not for initializations:

```javascript
var x = 5; // Initialize x

elem = document.getElementById("demo"); // Find an element 
elem.innerHTML = x + " " + y;           // Display x and y

var y = 7; // Initialize y
```
This code displays "5 undefined" because y's declaration is hoisted, but not its initialization to 7.

Best practice is to avoid bringing hoisting into play (which can be the source of bugs) by declaring all your variables at the top.

`"use strict"` at the top forces variables to be declared before they are used.
  
# Loops:
```javascript
  for (var i = 0; i < 10; i++) {
    document.write(i);
  }
```
```javascript
// Writes a 5 x table to web page.
var i = 0;
var msg = '';
while (i < 10) {
msg += i + ' x 5 = ' + (i * 5) + '<br />';
i++;
}
document.getElementById('answer').innerHTML = msg;
```
```javascript
var i = 0;
do {
// do stuff
i++;
} while (i < 10)
```

break; // leave the loop  
continue; // skip the rest of this iteration, go to next iteration of loop


# Objects:

## Literal Notation:
```javascript
var hotel = {
  name: 'Quay',
  rooms: 40,
  booked: 25,
  checkAvailability: function() {
    return this.rooms - this.booked;
  }
};

var hotel = {};
hotel.name = 'Quay';
hotel.rooms = 40;
hotel.booked = 25;
hotel.checkAvailability = function() {
  return this.rooms - this.booked;
};
```
## Constructor Notation:
```javascript  
var hotel = new Object();
hotel.name = 'Quay';
hotel.booked = 25;
hotel.checkAvailability = function() {
  return this.rooms - this.booked;
};

function Hotel(name, rooms, booked) {
  this.name = name;
  this.rooms = rooms;
  this.booked = booked;
  this.checkAvailability = function() {
    return this.rooms - this.booked;
  };
}
var quayHotel = new Hotel('Quay',40,25);
var parkHotel = new Hotel('Park',120,77);
```
    
## Adding and Removing (Deleting) Properties:
  
To add, just presumptively assign:
    
hotel.gym = true;
    
To remove (delete) a property:
    
delete hotel.booked;
      
## Built-In Objects:
Three types:
* Browser Object Model
* Document Object Model (DOM)
* Global Javascript Objects
    
### Browser Object Model:
Window
- Document (DOM)
- History
- Location
- Navigator
- Screen
        
Example properties of Window:  
window.innerHeight, window.innerWidth, window.document, window.history, window.history.length, window.screenX, window.screenY
        
Example methods of Window:  
window.alert(), window.open(), window.print()
        
### Document Object Model (DOM)
Example properties of window.document:  
document.title, document.URL, document.lastModified, document.domain
        
Example methods of window.document:  
document.write(), document.getElementById(), document.querySelectAll(), document.createElement(), document.createTextNode()
        
### Global Objects:
    
String:  
example property: length  
example methods: toUpperCase(), toLowerCase(), charAt(), indexOf(), substring(), split(), trim(), replace()
        
Number:  
example methods: isNaN(), toFixed(), toPrecision, toExponential()
        
Math:  
example property: Math.PI  
example methods: Math.round(), Math.sqrt(), Math.ceil(), Math.floor(), Math.random()
        
create a random number between 1 and 10:  
var randomNum = Math.floor((Math.random() * 10) + 1);
          
Date:  
example methods: getDate(), setDate(), getDay(), getFullYear(), getHours(), getTime(), getTimezoneOffset(), toDateString(), toTimeString(), toString()

var today = new Date(); // new Date() with no args returns current date & time  
var dayWeMet = new Date('May 7, 2000 20:00:00');  
var millisecsSinceMeeting = today - dayWeMet;  
var yearWeMet = dayWeMet.getFullYear();
    

Conditionals:
```javascript
if (expr) {

} else {

}

if (expr) {

} else if {

} else {

}


switch (level) {

case 'One':
  title = 'Level 1';
  break;

case 'Two':
  title = 'Level 2';
  break;

default:
  title = 'Test';
  break;

}
```
# Functions

## Named Functions:

```javascript  
function area(width, height) {
  return width * height;
}

var size = area(3,4);
```

The interpreter always goes through the entire script looking for all variable and function declarations _before_ executing the script line-by-line.  So a function created as a named function can be called in the script _before_ it has been declared.
    
## Anonymous Functions / Function Expressions:
  
If you put a function where the interpreter expects an expression, it's treated as an expression and is known as a _function_expression_. For a function expression, the name is usually omitted. A function with no name is an _anonymous_function_

```javascript    
var area = function(width, height) {
  return width * height;
};

var size = area(3,4);
```

In a function expression, the function isn't processed until the interpreter gets to that statement.  So you can't call an anonymous function before that interpreter has discovered it.  (This also means that any code that appears up to that point could potentially alter what happens inside this function.)
    
## IIFE ("Iffy" - Immediately-Invoked Function Expressions)
  
Often used to ensure that variable names don't conflict with each other, especially on pages that use more than one script.  
Used for code that only needs to run once in a task, rather than repeatedly called by other parts of the script.  
Any variables declared within the anonymous IIFE function are effectively protected from name collisions.
    
```javascript
var area = (function() {
  var width = 3;
  var height = 2;
  return width * height;
} () );
```
The last pair of parens tell the interpreter to execute the function immediately. The outermost grouping parens are there to ensure the interpreter treats the whole thing as an expression.
    
You may see the final pair of parens come after the outer grouping parens, but it's usually considered better practice to put them inside, as above.
    
## Methods on Data Types
### String
Turn a string into an array: split  
```javascript
// Take a string that includes newlines and turn it into an array where each element of the array is one line.  
var linesArray = inputText.split('\n'); // if inputText is '2\nHacker\nRank' then linesArray is ['2','Hacker','Rank']
```
Turn a string into an integer: parseInt
```javascript
var theInt = parseInt('1234');  // theInt == 1234
```

### Array
```javascript
// Create new array: 2 ways
var theArr = ['Hi','Dee','Ho']; // more common
var theArr = new Array('Hi','Dee','Ho');  // exactly the same, less common

// Size of array: length
var arr = [1,2,3];
var arrSize = arr.length; //=> 3
```
