# Developer Notes

---

> My Notes: For software development

A collection of write-ups on small things I learn day to day across a variety of languages and technologies. These are mostly things I learn about web development.

---

Table Of Contents:

1. [Debugging](#debugging)
2. [Basic Data Structures](#basic-data-structures)
3. [Object Oriented Programming Challenges](#oop)
4. [Functional Programming](#functional-programming)
5. [SASS](#sass)
6. [React](#react)

---


<div id="debugging"/>

## Debugging 

Table of Contents
1. [Intro to the Debugging Challenges](#1)
2. [Use typeof to Check the Type of a Variable](#2)
3. [Catching Misspelled Variable and Function Names](#3)
4. [Catch Unclosed Parentheses, Brackets, Braces and Quotes](#4)
5. [Catch Mixed Usage of Single and Double Quotes](#5)
6. [Catch Use of Assignment Operator Instead of Equality Operator](#6)
7. [Catch Missing Open and Closing Parenthesis After a Function Call](#7)
8. [Catch Off By One Errors When Using Indexing](#8)
9. [Use Caution When Re-initializing Variables Inside a Loop](#9)
10. [Prevent Infinite Loops with a Valid Terminal Condition](#10)

<div id="1"/>

### Intro to the Debugging Challenges

Debugging is the process of finding exactly what isn't working and fixing it.
These issues generally come in three forms:

1. syntax errors that prevent a program from running.
2. runtime errors when code fails to execute or has unexpected behavior.
3. semantic (or logical) errors when code doesn't do what it's meant to.

Example of syntax error - often detected by the code editor:

```
function willNotWork({
    console.log("Yuck");
}
// "function" keyword is misspelled and there's a missing parenthesis
```

Here's an example of a runtime error - often detected while the program executes:

```
function loopy() {
    while(true){
        console.log("Hello, World!");
    }
}
// Calling loopy starts an infinite loop, which may crash your browser
```

Example of a semantic error - often detected after testing code output:

```
function calcAreaOfReact(w,h) {
    return w + h; // This should be w * h
}
let myReactArea = calcAreaOfReact(2,3);
// Correct syntax and the program executes, but this gives the wrong answer
```

Debugging is frustrating but it helps to develop (and follow) a **step-by-step** approach to review your code.
This means checking the intermediate values and types of variables to see if they are what they should be.
You can start with simple process of elimination.

For example, if function A works and returns what its supposed to, the function B may have the issue. 
Or start checking values in a block of code from the middle to try to cut the search space in half. 
A problem in one spot indicates a bug in the first half of the code. If not, it's likely in the second.

This section will cover a couple helpful tools to find bugs, and some of the common forms the take.
Fortunately, debugging is a learnable skill that just requires a little patience and practice to master.


<div id="2"/>

### Use typeof to Check the Type of a Variable

You can use typeof to check the data structure, or type, of a variable. This is useful in debugging when working with multiple data types. If you can think you're adding two numbers, but one is actually a string, the results can be unexpected. Type errors can lurk in calculations or function calls. Be careful when you're accessing and working with external data in the form of a JavaScript Object Notation(JSON) object.

Here's are some examples using typeof:

```
console.log(typeof ""): // outputs "string"
console.log(typeof 0): // outputs "number"
console.log(typeof []): // outputs "object"
console.log(typeof {}): // outputs "object"

```

JavaScript recognizes six primitive (immutable) data types: 
Boolean,
Null,
Undefined,
Number,
String,
Symbol (new with ES6).

And one type for mutable items: 
Object.

Note that in JavaScript, arrays are technically a type of object.

```
let seven = 7;
let three = "3";
console.log(seven + three); // 73
// Add your code below this line
console.log(typeof seven); // Number
console.log(typeof three); // String
```

<div id="3"/>

### Catching Misspelled Variable and Function Names

The console.log() and typeof methods are the two primary ways to check intermediate values and types of program output. Now it's time to get into the common forms that bugs take. One syntax-level issue that fast typer's can commiserate with is the humble spelling error.

Transposed, missing, or mis-capitalized characters in a variable or function name will have the browser looking for an object that doesn't exist - and complain in the form of a reference error. JavaScript variable and function names are case-sensitive.

Fix the two spelling errors in the code so the netWorkingCapital calculation works.

```
let receivables = 10;
let payables = 8;
let netWorkingCapital = receivables - payable;
console.log(`Net working capital is: ${netWorkingCapital}`);
```

<div id="4"/>

### Catch Unclosed Parentheses, Brackets, Braces and Quotes

Another syntax error to be aware of is that all opening parentheses, brackets, curly braces, and quotes have a closing pair. Forgetting a piece tends to happen when you're editing existing code and inserting items with one of the pair types. Also, take care when nesting code blocks into others, such as adding a callback function as an argument to a method.

One way to avoid this mistake is as soon as the opening character is typed, immediately include the closing match, then move the curser back between them ans continue coding. Fortunately, most modern code editors generate the second half of the pair automatically.


<div id="5"/>

### Catch Mixed Usage of Single and Double Quotes

JavaScript allows the use of both single('') and double("") quotes to declare a string. Deciding which one to use generally comes down to personal preference, with some exceptions.
Having two choices is great when a string has contractions or another piece of text that's in quotes. just be careful that you don't close the string too early, which causes a syntax error.

Here are some examples of mixing quotes:

```
// These are correct:
const grouchoContraction = "I've had a perfectly wonderful evening, but this wasn't it.";
const quoteInString = "Groucho Marx once said 'Quote me as saying I was mis-quoted.'";
//This is incorrect:
const uhOhGroucho = 'I've had a perfectly wonderful evening, but this wasn't it.';
```

Of course, it is okay to use only one style of quotes. You can escape the quotes inside the string by using the backslash (\) escape character:

```
// Correct use of same quotes:
const allSameQuotes = 'I\'ve had a perfectly wonderful evening, but this wasn\'t it.';
```

<div id="6"/>

### Catch Use of Assignment Operator Instead of Equality Operator

Branching programs, i.e. ones that do different things if certain conditions are met, rely on if, else if, and else statements in JavaScript. The condition sometimes takes the form of testing whether a result is equal to a value.
The logic is spoken (in English, at least) as "if x equals y, then ..." which can literally translate into code using the =, or assignment operator. This leads to unexpected control flow in your program.

As covered in previous challenges, the assignment operator(=) in JavaScript assigns a value to a variable name. And the == and === operators check for equality (the triple === tests for strict equality, meaning both value and type are the same).

The code below assigns x to be 2, which evaluates as true. Almost every value on its own in JavaScript evaluates to true, except what are known as "falsy" values: false, 0, "" (an empty string), NaN, undefined, and null.

```
let x = 1;
let y = 2;
if (x = y) {
    // this code block will run for any value of y (unless y were originally set as a falsy)
} else {
    // this code block is what should run (but won't) in this example
}

```
```
let x = 7;
let y = 9;
let result = "to come";

if(x = y) {
  result = "Equal!";
} else {
  result = "Not equal!";
}

console.log(result);

// logs Equal!
// should log Not equal! 
// change the condition (x == y) || (x === y)
```

<div id="7"/>

### Catch Missing Open and Closing Parenthesis After a Function Call

When a function or method doesn't take any arguments, you may forget to include the (empty) opening and closing parenthesis when calling it. Often times the result of a function call is saved in a variable for other use in your code. This error can be detected by logging variable values (or their types) to the console and seeing that one is set to a function reference, instead of the expected value the function returns. 

The variables in the following example are different: 
```
function myFunction() {
    return "You Rock!";
}
let varOne = myFunction; // set to equal a function
let varTwo = myFunction(); // set to equal the string "You Rock!"
```

<div id="8"/>

### Catch Off By One Errors When Using Indexing

**Off by one error** (sometimes called OBOE) crop up when you're trying to target a specific index of a string or array (to slice or access a segment), or when looping over the indices of them. JavaScript indexing starts at zero, not one, which means the last index is always one less than the length of the item. If you try to access an index equal to the length, the program may throw an "index out of range" reference error or print undefined.

When you use string or array methods that take index ranges as arguments, it helps to read the documentation and understand  if they are inclusive (the item at the given index is part of what's returned) or not. Here are some examples of off by one errors.

```
let alphabet = "abcdefghijklmnopqrstuvwxyz";
let len = alphabet.length;
for (let i = 0; i <= len; i++) {
    // loops one too many times at the end
    console.log(alphabet[i]);
}
for (let j = 1; j < len; j++) {
    // loops one too few times and misses the first character at index 0
    console.log(alphabet[j]);
}
for (let k = 0; k < len; k++) {
    // Goldilocks approves - this is just right
    console.log(alphabet[k]);
}
```

<div id="9"/>

### Use Caution When Re-initializing Variables Inside a Loop

Sometimes it's necessary to save information, increment counters, or re-set variables within a loop. A potential issue is when variables either should be reinitialized, and aren't, or vice versa. This is particularly dangerous if you accidentally reset the variable being used for the terminal condition, causing an infinite loop.

Printing variable values with each cycle of your loop by using console.log() can uncover buggy behavior related to resetting, or failing to reset a variable.

The following function is supposed to create a two-dimensional array with m rows and n columns of zeros. Unfortunately, it's not producing the expected output because the row variable isn't being reinitialized (set back to an empty array) in the outer loop. Fix the code so it returns a correct 3x2 array of zeros, which looks like [[0,0], [0,0], [0,0]].

```
function zeroArray(m, n) {
  // Creates a 2-D array with m rows and n columns of zeroes
  let newArray = [];
  let row = [];
  for (let i = 0; i < m; i++) {
    // Adds the m-th row into newArray
    
    for (let j = 0; j < n; j++) {
      // Pushes n zeroes into the current row to create the columns
      row.push(0);
    }
    // Pushes the current row, which now has n zeroes in it, to the array
    newArray.push(row);
  }
  return newArray;
}

let matrix = zeroArray(3, 2);
console.log(matrix);
```
Answer:
```
function zeroArray(m, n) {
    // Creates a 2-D array with m rows and n columns of zeroes
    let newArray = [];
    
    for (let i = 0; i < m; i++) {
      // Adds the m-th row into newArray
      
      let row = []; /* <------ row has been declared inside the outer loop.
      Now a new row will be initialized during each iteration of the outer loop allowing 
      for the desired matrix. */
      console.log('row: ', row);
      for (let j = 0; j < n; j++) {
        // Pushes n zeroes into the current row to create the columns
        row.push(0);
        console.log('push ', row);
      }
      // Pushes the current row, which now has n zeroes in it, to the array
      newArray.push(row);
      console.log('newarray ', newArray);
    }
    return newArray;
  }
  
  let matrix = zeroArray(3, 2);
  console.log(matrix);

// output
row:  []
push  [ 0 ]
push  [ 0, 0 ]
newarray  [ [ 0, 0 ] ]
row:  []
push  [ 0 ]
push  [ 0, 0 ]
newarray  [ [ 0, 0 ], [ 0, 0 ] ]
row:  []
push  [ 0 ]
push  [ 0, 0 ]
newarray  [ [ 0, 0 ], [ 0, 0 ], [ 0, 0 ] ]
[ [ 0, 0 ], [ 0, 0 ], [ 0, 0 ] ]
```

<div id="10"/>

### Prevent Infinite Loops with a Valid Terminal Condition

The final topic is the dreaded infinite loop. Loops are great tools when you need your program to run a code block a certain number of times or until a condition is met, but they need a terminal condition that ends the looping. Infinite loops are likely to freeze or crash the browser, and cause general program execution mayhem, which no one wants.

There was an example of an infinite loop in the introduction to this section -it had no terminal condition to break out of the while loop inside loopy(). Do NOT call this function!

```
function loopy() {
    while(true) {
        console.log("Hello, world!");
    }
}
```
It's the programmer's job to ensure that the terminal condition, which tells the program when to break out of the loop code, is eventually reached. One error is incrementing or decrementing a counter variable in the wrong direction from the terminal condition. Another one is accidentally resetting a counter or index variable within the loop code, instead of incrementing or decrementing it.

The myFunc() function contains an infinite loop because the terminal condition i != 4 will never evaluate to false (and break the looping) -i will increment by 2 each pass, and jump right over 4 since i is odd to start. Fix the comparison operator in the terminal condition so the loop only runs for i less than or equal to 4.

```
function myFunc() {
  for (let i = 1; i != 4; i += 2) {  // i <=4;
    console.log("Still going!");
  }
}
```

---

<div id="basic-data-structures">

# Basic Data Structures

Table of contents
1. [Introduction](#id-section1)
2. [Use an Array to Store a Collection of Data](#id-section2)
3. [Access an Array's Contents Using Bracket Notation](#id-section3)
4. [Add Items to an Array with push() and unshift()](#id-section4)
5. [Remove Items from an Array with pop() and shift()](#id-section5)
6. [Remove Items Using splice()](#id-section6)
7. [Add Items Using splice()](#id-section7)
8. [Copy Array Items Using slice()](#id-section8)
9. [Copy an Array with the Spread Operator](#id-section9)
10. [Combine Arrays with the Spread Operator](#id-section10)
11. [Check For The Presence of an Element With indexOf()](#id-section11)
12. [Iterate Through All an Array's Items Using For Loops](#id-section12)
13. [Create complex multi-dimensional arrays](#id-section13)
14. [Add Key-Value Pairs to JavaScript Objects](#id-section14)
15. [Modify an Object Nested Within an Object](#id-section15)
16. [Access Property Names with Bracket Notation](#id-section16)
17. [Use the delete Keyword to Remove Object Properties](#id-section17)
18. [Check if an Object has a Property](#id-section18)
19. [Iterate Through the Keys of an Object with a for...in Statement](#id-section19)
20. [Generate an Array of All Object Keys with Object.keys()](#id-section20)
21. [Modify an Array Stored in an Object](#id-section21)




<div id="id-section1"/>

## Introduction

Data can be stored and accessed in many different ways, both in JavaScript and other languages. This section will teach you how to manipulate arrays, as well as access and copy the information within them. It will also teach you how to manipulate and access the data within JavaScript objects, using both dot and bracket notation. When you are done with this section, you should understand the basic properties and differences between arrays and objects, as well as how to choose which to use for a given purpose.

<div id="id-section2"/>

### Use an Array to Store a Collection of Data

The below is an example of the simplest implementation of an array data structure. This is known as a _one-dimensional array_, meaning it only has one level, or that it does not have any other arrays nested within it. Notice it contains _booleans, strings and numbers_, among other valid JavaScript data types:

```
let simpleArray = ['one', 2, 'three’, true, false, undefined, null];
console.log(simpleArray.length);
// logs 7
```
All array's have a length property, which as shown above can be very easily accessed with the syntax Array.length

A more complex implementation of an array can be seen below. This is known as a _multi-dimensional array_, or an array that contains other arrays. Notice that this array also contains JavaScript _objects_, which we will examine very closely in our next section, but for now, all you need to know is that arrays are also capable of storing complex objects.

```
let complexArray = [
  [
    {
      one: 1,
      two: 2
    },
    {
      three: 3,
      four: 4
    }
  ],
  [
    {
      a: "a",
      b: "b"
    },
    {
      c: "c",
      d: “d”
    }
  ]
];
```

<div id="id-section3"/>

### Access an Array's Contents Using Bracket Notation

The fundamental feature of any data structure is, of course, the ability to not only store data, but to be able to retrieve that data on command. So, now that we've learned how to create an array, let's begin to think about how we can access that array's information. 
When we define a simple array as seen below, there are 3 items in it:

```
let ourArray = ["a", "b", "c"];
```

In an array, each array item has an _index_. This index doubles as the position of that item in the array, and how you reference it. However, it is important to note, that JavaScript arrays are _zero-indexed_, meaning that the first element of an array is actually at the **zeroth** position, not the first.

In order to retrieve an element from an array we can enclose an index in brackets and append it to the end of an array, or more commonly, to a variable which references an array object. This is known as _bracket notation_.

For example, if we want to retrieve the "a" from ourArray and assign it to a variable, we can do so with the following code:

```
let ourVariable = ourArray[0];
// ourVariable equals "a"
```
In addition to accessing the value associated with an index, you can also set an index to a value using the same notation:

```
ourArray[1] = "not b anymore";
// ourArray now equals ["a", "not b anymore", "c"]
```

Using bracket notation, we have reset the item at index 1 from "b", to "not b anymore".

<div id="id-section4"/>

### Add Items to an Array with push() and unshift()

An array's length, like the data types it can contain, is not fixed. Arrays can be defined with a length of any number of elements, and elements can be added or removed over time;in other words, arrays are _mutable_. In this challenge, we will look at two methods with which we can programmatically modify an array: Array.push() and Array.unshift().

Both methods take one or more elements as parameters and add those elements to the array the method is being called on; the push() method adds elements to the end of an array, and unshift() adds elements to the beginning.
consider the following: 

```
let twentyThree = 'XXIII';
let romanNumerals = ['XXI', 'XXII'];

romanNumerals.unshift('XIX', 'XX');
// now equals ['XIX', 'XX', 'XXI', 'XXII']

romanNumerals.push(twentyThree);
// now equals ['XIX', 'XX', 'XXI', 'XXII', 'XXIII']
```
Notice that we can also pass variables, which allows us even greater flexibility in dynamically modifying our array's data.

<div id="id-section5"/>

### Remove Items from an Array with pop() and shift()

Both push() and unshift() have corresponding methods that are nearly functional opposites: pop() and shift(). As you may have guessed by now, instead of adding, pop() _removes_ an element from the end of an array, while shift() removes an element from the beginning. The key difference between pop() and shift() and their cousins push() and unshift(), is that neither method takes parameters, and each only allows an array to be modified by a single element at a time.

Let's take a look:

```
let greetings = ['what's up?', 'hello', 'see ya!'];

greetings.pop();
// now equals ['what's up?', 'hello']

greetings.shift();
// now equals ['hello']
```
We can also return the value of the removed element with either method like this:
```
let popped = greetings.pop();
// returns 'hello'
// greetings now equals []

```

<div id="id-section6"/>

### Remove Items Using splice()

Ok, so we've learned how to remove elements from the beginning and end of arrays using shift() and pop(), but what if we want to remove an element from somewhere in the middle? Or remove more than one element at once? Well, that's where splice() comes in. splice() allows us to do just that: **remove any number of consecutive elements** from anywhere in an array.

splice() can take up to 3 parameters, but for now, we'll focus on just the first 2. The first two parameters of splice() are integers which represent indexes, or positions, of the array that splice() is being called upon. And remember, arrays are _zero-indexed_, so to indicate the first-element of an array, we would use 0. splice()'s first parameter represents the index on the array from which to begin removing elements, while the second parameter indicates the number of elements to delete.For example:

```
let array = ['today', 'was', 'not', 'so', 'great'];
array.splice(2, 2);
// remove 2 elements beginning with the 3rd element
// array now equals ['today', 'was', 'great']
```

splice() not only modifies the array it's being called on, but it also returns a new array containing the value of the removed elements:

```
let array = ['I', 'am', 'feeling', 'really', 'happy'];
let newArray = array.splice(3, 2);
// newArray equals ['really', 'happy']
```

```
function sumOfTen(arr) {
  // change code below this line
  arr.splice(1, 2);
  // change code above this line
  return arr.reduce((a, b) => a + b);
}

// do not change code below this line
console.log(sumOfTen([2, 5, 1, 5, 2, 1]));
// returns 10
// arr.splice(1,2) counts 2 elements after element 1 so removes [0th, 1st, 2nd, 3rd, 4th, 5th] 2nd and 3rd elements from the array.
```

<div id="id-section7"/>

### Add Items Using splice()

With splice() - in addition to removing elements, we can use the third parameter, which represents one of more elements, to _add_ them as well. This can be useful for quickly switching out an element, or a set of elements, for another. For instance, lets say you're storing a color scheme for a set of DOM elements in an array, and want to dynamically change a color based on some action:

```
function colorChange(arr, index, newColor) {
  arr.splice(index, 1, newColor);
  return arr;
}

let colorScheme = ['#878787', '#a08794', '#bb7e8c', '#c9b6be', '#d1becf'];

colorScheme = colorChange(colorScheme, 2, '#332327');
// we have removed '#bb7e8c' and added '#332327' in its place
// colorScheme now equals ['#878787', '#a08794', '#332327', '#c9b6be', '#d1becf']
```

This function takes an array of hex values, an index at which to remove an element, and the new color to replace the removed element with. The return value is an array containing a newly modified color scheme!

<div id="id-section8"/>

### Copy Array Items Using slice()

slice(), rather than modifying an array, copies, or _extracts_, a given number of elements to a new array, leaving the array it is called upon untouched. 
slice() takes only 2 parameters 
- the first is the index at which to begin extraction
- the second is the index at which to stop extraction (extraction will occur up to, but not including the element at this index)
Consider this: 

```
let weatherConditions = ['rain', 'snow', 'sleet', 'hail', 'clear'];

let todaysWeather = weatherConditions.slice(1, 3);
// todaysWeather equals ['snow', 'sleet']
// weatherConditions still equals ['rain', 'snow', 'sleet', 'hail', 'clear']

```
In effect, we have created a new array by extracting elements from an existing array.

```
function forecast(arr) {
  // change code below this line
  let newArray = arr.slice(2, 4);
  return newArray;
}

// do not change code below this line
console.log(forecast(['cold', 'rainy', 'warm', 'sunny', 'cool', 'thunderstorms']));
```

<div id="id-section9"/>

### Copy an Array with the Spread Operator

While slice() allows us to be selective about what elements of an array to copy, among several other useful tasks, ES6's _new spread operator_ allows us to easily copy _all_ of an array's elements, in order, with a simple and highly readable syntax. The spread syntax looks like this: ...

In practice, we can use the spread operator to copy an array like so: 

```
let thisArray = [true, true, undefined, false, null];
let thatArray = [...thisArray];
// thatArray equals [true, true, undefined, false, null]
// thisArray remains unchanged, and is identical to thatArray
```
We have defined a function, copyMachine which takes arr (an array) and num (a number) as arguments. The function is supposed to return a new array made up of num copies of arr. We have done most of the work for you, but it doesn't work quite right yet. Modify the function using spread syntax so that it works correctly (hint: another method we have already covered might come in handy here!).
```
function copyMachine(arr, num) {
  let newArr = [];
  while (num >= 1) {
    // change code below this line
    // the unshift will take the [...arr] and add it as a single element inside the array each time // // num decrements.
    newArr.unshift([...arr]);
    // change code above this line
    num--;
  }
  return newArr;
}

// change code here to test different cases:
console.log(copyMachine([true, false, true], 4));
```

<div id="id-section10"/>

### Combine Arrays with the Spread Operator

Another huge advantage of the _spread_ operator, is the ability to combine arrays, or to insert all the elements of one array into another, at any index. With more traditional syntaxes, we can concatenate arrays, but this only allows us to combine arrays at the end of one, and at the start of another. Spread syntax makes the following operation extremely simple:

```
let thisArray = ['sage', 'rosemary', 'parsley', 'thyme'];

let thatArray = ['basil', 'cilantro', ...thisArray, 'coriander'];
// thatArray now equals ['basil', 'cilantro', 'sage', 'rosemary', 'parsley', 'thyme', 'coriander']

```
Using spread syntax, we have just achieved an operation that would have been more complex and more verbose had we used traditional methods.

We have defined a function spreadOut that returns the variable sentence, modify the function using the spread operator so that it returns the array ['learning', 'to', 'code', 'is', 'fun'].

```
function spreadOut() {
  let fragment = ['to', 'code'];
  let sentence = ['learning', ...fragment, 'is', 'fun']; // change this line
  return sentence;
}

// do not change code below this line
console.log(spreadOut());
```

<div id="id-section11"/>

### Check For The Presence of an Element With indexOf()

Since arrays can be changed, or _mutated_ at any time, there's no guarantee about where a particular piece of data will be on a given array, or if that element even still exists. Luckily, JavaScript provides us with another built-in method, indexOf(), that allows us to quickly and easily check for the presence of an element as a parameter, and when called, it returns the position, or index, of tht element, or -1 if the element does not exist on the array.

For example: 
```
let fruits = ['apples', 'pears', 'oranges', 'peaches', 'pears'];

fruits.indexOf('dates') // returns -1
fruits.indexOf('oranges') // returns 2
fruits.indexOf('pears') // returns 1, the first index at which the element exists
```
indexOf() can be incredibly useful for quickly checking for the presence of an element on an array. We have defined a function, quickCheck, that takes an array and an element as arguments. Modify the function using indexOf() so that it returns true if the passed element exists on the array, and false if it does not.

```
function quickCheck(arr, elem) {
  // change code below this line
  if (arr.indexOf(elem) == -1) {
    // return true;
    return false;
  }
  else {
    return true;
  }

  // change code above this line
}

// change code here to test different cases:
console.log(quickCheck([true, false, false], undefined));
```

<div id="id-section12"/>

### Iterate Through All an Array's Items Using For Loops

Sometimes when working with arrays, it is very handy to be able to iterate through each item to find one or more elements that we might need, or to manipulate an array based on which data items meet a certain set of criteria. JavaScript offers several built in methods that each iterate over arrays in slightly different ways to achieve different results (such as **every(), forEach(), map(), etc**), however the technique which is most flexible and offers us the greatest amount of control is a simple for loop.

Consider the following: 

```
function greaterThenTen(arr) {
  let newArr = [];
  for (let i = 0; i < arr.length; i++) {
    if(arr[i] > 10) {
      newArr.push(arr[i]);
    }
  }
  return newArr;
}

greaterThanTen([2, 12, 8, 14, 80, 0, 1]);
// returns [12, 14, 80]
```
Using a for loop, this function iterates through and accesses each element of the array, and subjects it to a simple test that we have created. In this way, we have easily and programmatically determined which data items are greater than 10, and returned a new array containing those items.

We have defined a function, filteredArray, which takes arr, a nested array, and elem as arguments, and returns a new array. elem represents an element that may or may not be present on one or more of the arrays nested within arr. Modify the function, using a for loop, to return a filtered version of the passed array such that any array nested within arr containing elem has been removed.

```
function filteredArray(arr, elem) {
  let newArr = [];
  // change code below this line
  for (let i = 0; i < arr.length; i++) {
    // console.log(arr[i].indexOf(elem));
    if (arr[i].indexOf(elem) == -1) {
      // console.log(arr[i]);
      newArr.push(arr[i]);
    }
  }
  // change code above this line
  return newArr;
}

// change code here to test different cases:
console.log(filteredArray([[3, 2, 3], [1, 6, 3], [3, 13, 26], [19, 3, 9]], 3));
```

<div id="id-section13"/>

### Create complex multi-dimensional arrays

Awesome! You have just learnt a ton about arrays! This has been a fairly high level overview, and there is plenty more to learn about working with arrays, much of which you will see in later sections. But before moving on to looking at _Objects_ lets take one more look, and see how arrays can become a bit more complex than what we have seen in previous challenges.

One of the most powerful features when thinking of arrays as data structures, is that arrays can contain, or even be completely make up of other arrays. We have seen arrays that contain arrays in previous challenges, but fairly simple ones. However, arrays can contain an infinite depth of arrays that can contain other arrays, each with their own arbitrary levels of depth, and so on. In this way, an array can very quickly become very complex data structure, known as a _multi-dimensional_, or nested array. 
Consider the following example:

```
let nestedArray = [ // top, or first level - the outer most array
  ['deep], // an array within an array, 2 levels of depth
  [
    ['deeper'], ['deeper'] // 2 arrays nested 3 levels deep
  ],
  [
    [
      ['deepest'], ['deepest'] // 2 arrays nested 4 levels deep
    ],
    [
      [
        ['deepest-est?] // an array nested 5 levels deep
      ]
    ]
  ]
];

```
While this example may seem convoluted, this level of complexity is not unheard of, or even unusual, when dealing with large amounts of data.

However, we can still very easily access the deepest levels of an array this complex with bracket notation:

```
console.log(nestedArray[2][1][0][0][0]);
// logs: deepest-est?
```
And now that we know where that piece of data is, we can reset it if we want to:

```
nestedArray[2][1][0][0][0] = 'deeper still';
// now logs: deeper still
```
We have defined a variable, myNestedArray, set equal to an array. Modify myNestedArray, using any combination of strings, numbers, and booleans for data elements, so that it has exactly five levels of depth (remember, the outer-most array is level 1). Somewhere on the third level, include the string 'deep', on the fourth level, include the string 'deeper', and on the fifth level, include the string 'deepest'.

```
let myNestedArray = [
  // change code below this line
  ['unshift', false, 1, 2, 3, 'complex', 'nested'],
  ['loop', 'shift', 6, 7, 1000, 'method'],
  ['concat', false, true, 'spread', 'array'],
  ['mutate', 1327.98, 'splice', 'slice', 'push'],
  ['iterate', 1.3849, 7, '8.4876', 'arbitrary', 'depth', 
  [['deep'], [3],[['deeper'], [4], [['deepest'], [5]]]]]
  // change code above this line
];

console.log(myNestedArray);
```

<div id="id-section14"/>

### Add Key-Value Pairs to JavaScript Objects

At their basic, objects are just collections of _key-value pairs_, or in other words, pieces of data mapped to unique identifies that we cal _properties_ or _keys_. Let's take a look at a very simple example.

```
let FCC_User = {
  username: 'awesome_coder',
  followers: 572,
  points: 1741,
  completedProjects: 15
};
```
The above code defines an object called FCC_User that has four _properties_ each of which map to a specific value. If we wanted to know the number of followers FCC_Users has, we can access that property by writing:

```
let userData = FCC_User.followers;
// userData equals 572
```
This is called _dot notation_. Alternatively, we can also access the property with brackets, like so:
```
let userData = FCC_User['followers']
// userData equals 572
```
Notice that with _bracket notation_, we enclosed followers in quotes. This is because the brackets actually allow us to pass a variable in to be evaluated as a property name(hint: keep this in mind for later!). Had we passed followers in without the quotes, the JavaScript engine would have attempted to evaluate it as a variable, and a **ReferenceError: followers is not defined** would have been thrown.

Using the same syntax, we can also add new key-value pairs to objects. We've created a foods object with three entries. Add three more entries: bananas with a value of 13, grapes with a value of 35, and strawberries with a value of 27.

```
let foods = {
  apples: 25,
  oranges: 32,
  plums: 28
};

// change code below this line
foods.bananas = 13;
foods.grapes = 35;
foods.strawberries = 27;
// change code above this line

console.log(foods);
```
or
```
let foods = {
  apples: 25,
  oranges: 32,
  plums: 28
};
// change code below this line
foods['bananas'] = 13;
foods['grapes'] = 35;
foods['strawberries'] = 27;
// change code above this line
console.log(foods);
```

* The foods object has already been declared. All that is left to be done is to add three new key-values.

```
OBJECT[{KEY}] = {VALUE}
```

<div id="id-section15"/>

### Modify an Object Nested Within an Object

Now let's take a look at a slightly more complex object. Object properties can be nested to an arbitrary depth, and their values can be any type of data supported by JavaScript, including arrays and even other objects. Consider the following:

```
let nestedObject = {
  id: 28802695164,
  date: 'December 31, 2016',
  data: {
    totalUsers: 99,
    online: 80,
    onlineStatus: {
      active: 67,
      away: 13
    }
  }
};
```
nestedObjects has three unique keys: id, whose value is a number, date whose value is a string, and data, whose value is an object which has yet another object nested within it. While structures can quickly become complex, we can still use the same notations to access the information we need.

Here we've defined an object, userActivity, which includes another object nested within it. You can modify properties on this nested object in the same way you modified properties in the last challenge. Set the value of the online key to 45

```
let userActivity = {
  id: 23894201352,
  date: 'January 1, 2017',
  data: {
    totalUsers: 51,
    online: 42
  }
};

// change code below this line
userActivity.data.online = 45;
// change code above this line

console.log(userActivity);
```

Method: 
Remember the object you want to change is two levels deep, dot-notation is easier to use in this instance.
Simply define the object and then use dot-notation to access the second object and finally the final element you width to modify.

```
let myObject = {
  level_1: 'outside',
  first_level_object: {
    level_2: '2 levels deep',
    second_level_object: {
      level_3: '3 levels deep'
      }
   }
};
//The following line of code will modify the data found in level_2.
myObject.first_level_object.level_2 = 'level-2 has been reached';
```

<div id="id-section16"/>

### Access Property Names with Bracket Notation

You can use bracket notation as a way to access property values using the evaluation of a variable. For instance, imagine that our foods object is being used in a program for a supermarket cash register. We have some function that sets the selectedFood and we want to check our foods object for the presence of that food. This might look like:

```
let selectedFood = getCurrentFood(scannedItem);
let inventory = foods[selectedFood];
```

This code will evaluate the value stored in the selectedFood variable and return the value of that key in the foods object, or undefined if it is not present. Bracket notation is very useful because sometimes object properties are not known before runtime or we need to access them in more dynamic way.

We've defined a function, checkInventory, which receives a scanned item as an argument. Return the current value of the scannedItem key in the foods object. You can assume that only valid keys will be provided as an argument to checkInventory.

```
let foods = {
  apples: 25,
  oranges: 32,
  plums: 28,
  bananas: 13,
  grapes: 35,
  strawberries: 27
};
// do not change code above this line

function checkInventory(scannedItem) {
  // change code below this line

}

// change code below this line to test different cases:
console.log(checkInventory("apples"));
```

Method:
  * Using bracket notation simply write the return statement in the checkInventory() function.
  * The following code block demonstrates the required syntax

```
let juice = {
  apple: 1.15,
  orange: 1.45
};     
function checkInventory(scannedItem) {
  return juice[scannedItem];
}

```

<div id="id-section17"/>

### Use the delete Keyword to Remove Object Properties

Now you know what objects are and their basic features and advantages. In short, they are key-value stores which provide a flexible, intuitive way to structure data, **and**, they provide very fast lookup time. 
Here we will see how to remove a key-value pair from an object.

Let's revisit our foods object example one last time. If we wanted to remove the apples key, we can remove it by using the delete keyword like this:

```
delete foods.apples;
```

<div id="id-section18"/>

### Check if an Object has a Property

Now we can add, modify, and remove keys from objects. But what if we just wanted to know if an object has a specific property? JavaScript provides us with two different ways to do this. One uses the hasOwnProperty() method and the other uses the **in** keyword. If we have an object users with a property of Alan, we could check for its presence in either of the following way: 

```
users.hasOwnProperty('Alan');
'Alan' in users;
// both return true
```
We've created an object, users, with some users in it and a function isEveryoneHere, which we pass the users object to as an argument. Finish writing this function so that it returns true only if the users object contains all four names, Alan, Jeff, Sarah, and Ryan, as keys, and false otherwise.

```
let users = {
  Alan: {
    age: 27,
    online: true
  },
  Jeff: {
    age: 32,
    online: true
  },
  Sarah: {
    age: 48,
    online: true
  },
  Ryan: {
    age: 19,
    online: true
  }
};

function isEveryoneHere(obj) {
  // change code below this line
  return obj.hasOwnProperty('Alan', 'Jeff', 'Sarah', 'Ryan');
  // change code above this line
}

console.log(isEveryoneHere(users));
```

Method:
  * The simplest way to complete this challenge is to create an if-statement to check wether or not the object contains all users, then to return a true or false statement. The first solution does just this.
  * The second solution works in exactly the same way, only it uses 1 line of code - Conditional(ternary)-Operator - within the function.

Solution-1:
```
let users = {
  Alan: {
    age: 27,
    online: true
  },
  Jeff: {
    age: 32,
    online: true
  },
  Sarah: {
    age: 48,
    online: true
  },
  Ryan: {
    age: 19,
    online: true
  }
};

function isEveryoneHere(obj) {
  // change code below this line
  if(users.hasOwnProperty('Alan','Jeff','Sarah','Ryan')) {
    return true;
  }
  return false;
  // change code above this line
}

console.log(isEveryoneHere(users));
```

Solution-2;
```
function isEveryoneHere(obj) {
  return (users.hasOwnProperty('Alan','Jeff','Sarah','Ryan')) ? true : false;
}
```

<div id="id-section19"/>

### Iterate Through the Keys of an Object with a for...in Statement

Sometimes you may need to iterate through all the keys within an object. This requires a specific syntax in JavaScript called a for...in statement. For our users object, this could look like:

```
for (let user in users) {
  console.log(user);
};

// logs:
Alan
Jeff
Sarah
Ryan
```

In this statement, we defined a variable user, and as you can see, this variable was reset during each iteration to each of the object's keys as the statement looped through the object, resulting in each user's name being printed to the console.

NOTE:
Objects do not maintain an ordering to stored keys like arrays do; thus a keys position on an object, or the relative order in which it appears, is irrelevant when referencing or accessing that key.

We've defined a function, countOnline; use a for...in statement within this function to loop through the users in the users object and return the number of users whose online property is set to true.

```
let users = {
  Alan: {
    age: 27,
    online: false
  },
  Jeff: {
    age: 32,
    online: true
  },
  Sarah: {
    age: 48,
    online: false
  },
  Ryan: {
    age: 19,
    online: true
  }
};

function countOnline(obj) {
  // change code below this line
  let count = 0;
  for (let prop in obj) {
    if (obj[prop]online === true) {
      count++;
    }
  }
  return count;
  // change code above this line
}

console.log(countOnline(users));
```

<div id="id-section20"/>

### Generate an Array of All Object Keys with Object.keys()

We can also generate an array which contains all the keys stored in an object using the Object.keys()
method and passing in an object as the argument. This will return an array with strings representing each property in the object. Again, there will be no specific order to the entries in the array.

Finish writing the getArrayOfUsers function so that it returns an array containing all the properties in the object it receives as an argument.

```
let users = {
  Alan: {
    age: 27,
    online: false
  },
  Jeff: {
    age: 32,
    online: true
  },
  Sarah: {
    age: 48,
    online: false
  },
  Ryan: {
    age: 19,
    online: true
  }
};

function getArrayOfUsers(obj) {
  // change code below this line
  return Object.keys(obj);
  // change code above this line
}

console.log(getArrayOfUsers(users));
```

<div id="id-section21"/>

### Modify an Array Stored in an Object

Now you've seen all the basic operations for JavaScript objects. You can add, modify, and remove key-value pairs, check if keys exist, and iterate over all the keys in an object. As you continue learning JavaScript you will see even more versatile applications of objects. Additionally, the optional Advanced Data Structures lessons later in the curriculum also cover the ES6 _Map_ and _Set_ objects, you're fully prepared to begin tackling more complex problems using JavaScript!

Take a look at the object we've provided in the code editor. The user object contains three keys. The data key contains five keys, one of which contains an array of friends. From this, you can see how flexible objects are as data structures. We've started writing a function addFriend. Finish writing it so that it takes a user object and adds the name of the friend argument to the array stored in user.data.friends and returns that array.

```
let user = {
  name: 'Kenneth',
  age: 28,
  data: {
    username: 'kennethCodesAllDay',
    joinDate: 'March 26, 2016',
    organization: 'freeCodeCamp',
    friends: [
      'Sam',
      'Kira',
      'Tomo'
    ],
    location: {
      city: 'San Francisco',
      state: 'CA',
      country: 'USA'
    }
  }
};
function addFriend(userObj, friend) {
  // change code below this line  
  userObj.data.friends.push(friend);
  return userObj.data.friends;
  
  // change code above this line
}
console.log(addFriend(user, 'Pete'));
```
Method:

    The function can be written in just two lines of code.
    The first line should just use the push() function to add the friendparameter to the array found in user.data.friend. The second line will return the modified array.
    Remember that user must be referenced with the first parameter given to the addFriend() function.

---

<div id="oop">

# Object Oriented Programming Challenges

Table of Contents
1. [Introduction](#id-1)
2. [Create a Basic JavaScript Object](#id-2)
3. [Use Dot Notation to Access the Properties of an Object](#id-3)
4. [Create a Method on an Object](#id-4)
5. [Make Code More Reusable with the this Keyword](#id-5)
6. [Define a Constructor Function](#id-6)
7. [Use a Constructor to Create Objects](#id-7)
8. [Extend Constructors to Receive Arguments](#id-8)
9. [Verify an Object's Constructor with instanceof](#id-9)
10. [Understand Own Properties](#id-10)
11. [Use Prototype Properties to Reduce Duplicate Code](#id-11)
12. [Iterate Over All Properties](#id-12)
13. [Understand the Constructor Property](#id-13)
14. [Change the Prototype to a New Object](#id-14)
15. [Remember to Set the Constructor Property when Changing the Prototype](#id-15)
16. [Understand Where an Object’s Prototype Comes From](#id-16)
17. [Understand the Prototype Chain](#id-17)
18. [Use Inheritance So You Don't Repeat Yourself](#id-18)
19. [Inherit Behaviors from a Supertype](#id-19)
20. [Set the Child's Prototype to an Instance of the Parent](#id-20)
21. [Reset an Inherited Constructor Property](#id-21)
22. [Add Methods After Inheritance](#id-22)
23. [Override Inherited Methods](#id-23)
24. [Use a Mixin to Add Common Behavior Between Unrelated Objects](#id-24)
25. [Use Closure to Protect Properties Within an Object from Being Modified Externally](#id-25)
26. [Understand the Immediately Invoked Function Expression (IIFE)](#id-26)
27. [Use an IIFE to Create a Module](#id-27)


<div id="id-1"/>

### Introduction

As its name implies, object oriented programming organizes code into object definitions. These are sometimes called classes, and they group together data with related behavior. The data is an object's attributes, and the behavior (or functions) are methods.

The object structure makes it flexible within a program. Objects can transfer information by calling and passing data to another object's methods. Also, new classes can receive, or inherit, all the features from a base or parent class. This helps to reduce repeated code.

Your choice of programming approach depends on a few factors. These include the type of problem, as well as how you want to structure your data and algorithms. This section covers object oriented programming principles in JavaScript.

<div id="id-2"/>

### Create a Basic JavaScript Object

Think about things people see everyday, like cars, shops, and birds. These are all objects: tangible things people can observe and interact with.

What are some qualities of these objects? A car has wheels. Shops sell items. Birds have wings.

These qualities or properties, define what makes up an object. Note that similar objects share the same properties, but may have different values for those properties. For example, all cars have wheels, but not all cars have the same number of wheels.

Objects in JavaScript are used to model real-world objects, giving them properties and behavior just like their real-world counterparts. Here's an example using these concepts to create a duck object:

```
let duck = {
    name: "Aflac", 
    numLegs: 2
};
```
This duck object has two property/value pairs: a name of "Aflac" and a numLegs of 2.

<div id="id-3"/>

### Use Dot Notation to Access the Properties of an Object

How to access the values of those properties.

```
let duck = {
    name: "Aflac",
    numLegs: 2
};
console.log(duck.name);
// This prints "Aflac" to the console
```
Dot notation is used on the object name, duck, followed by the name of the property, name, to access the value of "Aflac"

<div id="id-4"/>

### Create a Method on an Object

Objects can have a special type of property, called a method.

Methods are properties that are functions. This adds different behavior to an object. Here is the duck example with a method: 

```
let duck = {
    name: "Aflac",
    numLegs: 2,
    sayName: function() {return "The name of this duck is " + duck.name + ".";}
};
duck.sayName();
// Returns "The name of this duck is Aflac
```

This example adds the sayName method, which is a function that returns a sentence giving the name of the duck.
Notice that the method accessed the name property in the return statement using duck.name. The next challenge will cover another way to do this.

<div id="id-5"/>

### Make Code More Reusable with the this Keyword

While the above example is a valid way to access the object's property, there is a pitfall here. If the variable name changes, any code referencing the original name would need to be updated as well. In a short object definition, it isn't a problem, but if an object has many references to its properties there is a greater chance for error.

A way to avoid these issues is with the this keyword:
```
let duck = {
    name: "Aflac",
    numLegs: 2,
    sayName: function() {return "The name of this dick is " + this.name + ".";}
};
```

this is a deep topic, and the above example is only one way to use it. In the current context, this refers to the object that the method is associated with: duck.

If the object's name is changed to mallard, it is not necessary to find all the references to duck in the code. It makes the code reusable and easier to read.

<div id="id-6"/>

### Define a Constructor Function

Constructors are functions that create new objects. They define properties and behaviors that will belong to the new object. Think of them as a blueprint for the creation of new objects.

Here is an example of a constructor:
```
function Bird() {
    this.name = "Albert";
    this.color = "blue";
    this.numLegs = 2;
}
```
This constructor defines a Bird object with properties name, color, and numLegs set to Albert, blue, and 2, respectively.

Constructors follow a few conventions:

    * Constructors are defined with a capitalized name to distinguish them from other functions that are not constructors.
    * Constructors use the keyword _this_ to set properties of the object they will create. Inside the constructor, _this_ refers to the new object it will create.
    * Constructors define properties and behaviors instead of returning a value as other functions might.

<div id="id-7"/>

### Use a Constructor to Create Objects

Here's the Bird constructor from the above challenge:

```
function Bird() {
    this.name = "Albert";
    this.color = "blue";
    this.numLegs = 2;
    // "this" inside the constructor always refers to the object being created
}

let blueBird = new Bird();
```
Notice the _new_ operator is used when calling a constructor. This tells JavaScript to create a new instance of Bird called blueBird. Without the new operator, this inside the constructor would not point to the newly created object, giving unexpected results.

Now blueBird has all the properties defined inside the Bird constructor:
```
blueBird.name;  // => Albert
blueBird.color; // => blue
blueBird.numLegs;   // => 2
```
Just like any other object, its properties can be accessed and modified.

```
blueBird.name = 'Elvire';
blueBird.name; // => Elvira
```

<div id="id-8"/>

### Extend Constructors to Receive Arguments

The Bird and Dog constructors from above worked well. However, notice that all Birds that are created with the Bird constructor are named Albert, are blue in color, and have two legs. What if you want birds with different values for name and color? It's possible to change the properties of each bird manually but that would be a lot of work:
```
let swan = new Bird();
swan.name = "Carlos";
swan.color = "White";
```
Suppose you were writing a program to keep track of hundreds or even thousands of different birds in an aviary. It would take a lot of time to create all the birds, then change the properties to different values for every one.

To more easily create different Bird objects, you can design your Bird constructor to accept parameters:
```
function Bird(name, color) {
    this.name = name;
    this.color = color;
    this.numLegs = 2;
}
```
Then pass in the values as arguments to define each unique bird into the Bird constructor:

```
let cardinal = new Bird("Bruce", "red");
```
This gives a new instance of Bird with name and color properties set to Bruce and red, respectively. The numLegs property is still set to 2.

The cardinal has these properties:
```
cardinal.name // Bruce
cardinal.color // red
cardinal.numLegs // 2
```

The constructor is more flexible. It's now possible to define the properties for each Bird at the time it is created, which is one way that JavaScript constructors are so useful. They group objects together based on shared characteristics and behavior and define a blueprint that automates their creation.

<div id="id-9"/>

### Verify an Object's Constructor with instanceof

Anytime a constructor function creates a new object, that object is said to be an instance of its constructor. JavaScript gives a convienient way to verify this with the instanceof operator. instanceof allows you to compare an object to a constructor, returning true or false based on whether or not that object was created with the constructor. Here's an example:

```
let Bird = function(name, color) {
    this.name = name;
    this.color = color;
    this.numLegs = 2;
}

let crow = new Bird("Alexis", "black");

crow instanceof Bird;   // => true
```
If an object is created using a constructor, instanceof will verify that  it is not an instance of that constructor:

```
let canary = {
    name: "Mildred",
    color: "Yellow",
    numLegs: 2
};

canary instanceof Bird; // => false
```

<div id="id-10"/>

### Understand Own Properties

In the following example, the Bird constructor defines two properties: name and numLegs:

```
function Bird(name) {
    this.name = name;
    this.numLegs = 2;
}

let duck = new Bird("Donald");
let canary = new Bird("Tweety");

```

name and numLegs are called own properties, because they are defined directly on the instance object. That means that duck and canary each has its own separate copy of these properties. 

In fact every instance of Bird will have its own copy of these properties.

The following code adds all of the own properties of duck to the array ownProps:
```
let ownProps = [];

for (let property in duck) {
    if (duck.hasOwnProperty(property)) {
        ownProps.push(property);
    }
}

console.log(ownProps); // prompts ["name", "numLegs"]
```
Add the own properties  of canary to the array ownProps

```
function Bird(name) {
    this.name = name;
    this.numLegs = 2; 
}

let canary = new Bird("Tweety");
let ownProps = [];

for (let property in canary) {
    if(canary.hasOwnProperty(property)) {
        ownProps.push(property);
    }
}
```

<div id="id-11"/>

### Use Prototype Properties to Reduce Duplicate Code

Since numlegs will probably have the same value for all instances of Bird, you essentially have a duplicate variable numLegs inside each Bird instance.

This may not be an issue when there are only two instances, but imagine if there are millions of instances. That would be a lot of duplicate variables.

A better way is to use Bird's prototype. The prototype is an object that is shared among ALL instances of Bird. Here's how to add numLegs to the Bird prototype:

```
Bird.prototype.numLegs = 2;
```
Now all instances of Bird will have the numLegs property.

```
console.log(duck.numLegs); // prints 2
console.log(canary.numLegs); // prints 2
```
Since all instances automatically have the properties on the prototype, think of a prototype as a "recipe" for creating objects.

Note that the prototype for duck and canary is part of the Bird constructor as Bird.prototype. Nearly every object in JavaScript has a prototype property which is part of the constructor function that created it.

<div id="id-12"/>

### Iterate Over All Properties

You have now seen two types of properties:
    own properties and prototype properties.
Own properties are defined directly on the object instance itself.
Prototype properties are defined on the prototype

```
function Bird(name) {
    this.name = name;   // own property
}

Bird.prototype.numLegs = 2; // prototype property

let duck = new Bird("Donald");
```
Here is how you add duck's own properties to the array ownProps and prototype properties to the array prototypeProps:

```
let ownProps = [];
let prototypeProps = [];

for (let property in duck) {
    if (duck.hasOwnProperty(property)) {
        ownProps.push(property);
    } else {
        prototypeProps.push(property);
    }
}

console.log(ownProps); // prints ["name"]
console.log(prototypeProps); // prints ["numLegs"]
```
Add all of the own properties of beagle to the array ownProps. Add all of the prototype properties of Dog to the array prototypeProps.

```
function Dog(name) {
  this.name = name;
}

Dog.prototype.numLegs = 4;

let beagle = new Dog("Snoopy");

let ownProps = [];
let prototypeProps = [];

// Add your code below this line

for (let property in beagle) {
    if (beagle.hasOwnProperty(property)) {
        ownProps.push(property);
    } else {
        prototypeProps.push(property);
    }
}
```

<div id="id-13"/>

### Understand the Constructor Property

There is a special constructor property located on the object instances duck and beagle that were created in the previous challenges:

```
let duck = new Bird();
let beagle = new Dog();

console.log(duck.constructor === Bird); // prints true
console.log(beagle.constructor === Dog);    // prints true
```

Note the constructor property is a reference to the constructor function that created the instance.

The advantage of the constructor property is that it's possible to check for this property to find out what kind of object it is. Here's an example of how this could be used:

```
function joinBirdFraternity(candidate) {
    if (cindidate.constructor === Bird) {
        return true;
    } else {
        return false;
    }
}
```
**Note**
Since the constructor property can be overwritten (which will be covered in the next two challenges) it's generally better to use the instanceof method to check the type of an object.

Write a joinDogFraternity function that takes a candidate parameter and, using the constructor property, return true id the candidate is a Dog, otherwise return false.

```
function Dog(name) {
    this.name = name;
}

// Add your code below this line
function joinDogFraternity(candidate) {
    if (candidate.constructor === Dog) {
        return true;
    } else {
        return false;
    }
}
```

<div id="id-14"/>

### Change the Prototype to a New Object

Up until now we have been adding properties to the prototype individually:

```
Bird.prototype.numlegs = 2;
```
This becomes tedious after more than a few properties.
```
Bird.prototype.eat = function() {
    console.log("nom nom nom")*;
}

Bird.prototype.describe = function() {
    console.log("My name is " + this.name);
}
```
A more efficient way is to set the prototype to a new object that already contains the properties. This way, the properties are added all at once:
```
Bird.prototype = {
    numLegs: 2,
    eat: function() {
        console.log("nom nom nom");
    },
    describe: function() {
        console.log("My name is " + this.name);
    }
};
```
Add the property numLegs and the two methods eat() and describe() to the prototype of Dog by setting the prototype to a new object.

```
function Dog(name) {
  this.name = name; 
}

Dog.prototype = {
  // Add your code below this line
  numLegs: 2,
  eat: function() {
      console.log("nom nom nom");
  },
  describe: function() {
      console.log("My name is " + this.name);
  }
};
```

<div id="id-15"/>

### Remember to Set the Constructor Property when Changing the Prototype

There is one crucial side effect of manually setting the prototype to a new object. It erased the constructor property! The code in the previous challenge would print the following for duck:

```
console.log(duck.constructor)
// prints 'undefined' - Oops!
```
To fix this, whenever a prototype is manually set to a new object, remember to define the constructor property:

```
Bird.prototype = {
    constructor: Bird,  // define the constructor property
    numLegs: 2,
    eat: function() {
        console.log("nom nom nom");
    },
    describe: function() {
        console.log("My name is " + this.name);
    }
};
```
Define the constructor property on the Dog prototype

```
function Dog(name) {
  this.name = name; 
}

// Modify the code below this line
Dog.prototype = {
  constructor: Dog,
  numLegs: 2, 
  eat: function() {
    console.log("nom nom nom"); 
  }, 
  describe: function() {
    console.log("My name is " + this.name); 
  }
};

```

<div id="id-16"/>

### Understand Where an Object’s Prototype Comes From

Just like people inherit genes from their parents, an object inherits its prototype directly from the constructor function that created it. For example, here the Bird constructor creates the duck object:

```
function Bird(name) {
    this.name = name;
}

let duck = new Bird("Donald");
```

duck inherits its prototype from the Bird constructor function. You can show this relationship with the isPrototypeOf method:

```
Bird.prototype.isPrototypeOf(duck);
// returns true
```
Use isPrototypeOf to check the prototype of beagle.

```
function Dog(name) {
  this.name = name;
}

let beagle = new Dog("Snoopy");

// Add your code below this line
Dog.prototype.isPrototypeOf(beagle);
```

<div id="id-17"/>

### Understand the Prototype Chain

All objects in JavaScript (with a few exceptions) have a prototype. Also, an object's prototype itself is an object.
```
function Bird(name) {
    this.name = name;
}

typeof Bird.prototype; // => object
```
Because a prototype is an object, a prototype can have its own prototype! In this case, the prototype of Bird.prototype is Object.prototype:

```
Object.prototype.isPrototypeOf(Bird.prototype);
// returns true
```

How is this useful? You may recall the hasOwnProperty method from a previous challenge:

```
let duck = new Bird("Donald");
duck.hasOwnProperty("name"); // => true
```
The hasOwnProperty method is defined in Object.prototype, which can be accessed by Bird.prototype, which can then be accessed by duck. This is an example of the prototype chain.

In this prototype chain, Bird is the _supertype_ for duck, while duck is the _subtype_. Object is a supertype for both Bird and duck.

Object is a supertype for all objects in JavaScript. Therefore, any object can use the hasOwnProperty method.

Modify the code to show the correct prototype chain.

```
function Dog(name) {
  this.name = name;
}

let beagle = new Dog("Snoopy");

Dog.prototype.isPrototypeOf(beagle);  // => true

// Fix the code below so that it evaluates to true
Object.prototype.isPrototypeOf(Dog.prototype);
```

<div id="id-18"/>

### Use Inheritance So You Don't Repeat Yourself

There's a principle in programming called Don't Repeat Yourself (DRY). The reason repeated code is a problem is because any chance requires fixing code in multiple places. This usually means more work for programmers and more room for errors.

Notice in the example below that the describe method is shared by Bird and Dog:

```
Bird.prototype = {
  constructor: Bird,
  describe: function() {
    console.log("My name is " + this.name);
  }
};

Dog.prototype = {
  constructor: Dog,
  describe: function() {
    console.log("My name is " + this.name);
  }
};
```

The describe method is repeated in two places. The code can be edited to follow the DRY principle by creating a supertype(or parent) called Animal:

```
function Animal() {};

Animal.prototype = {
    constructor: Animal,
    describe: function() {
        console.log("My name is " + this.name);
    }
};
```
Since Animal includes the describe method, you can remove it from Bird and Dog

```
Bird.prototype = {
  constructor: Bird
};

Dog.prototype = {
  constructor: Dog
};
```

The eat method is repeated in both Cat and Bear. Edit the code in the spirit of DRY by moving the eat method to the Animal supertype.

```
function Cat(name) {
  this.name = name; 
}

Cat.prototype = {
  constructor: Cat, 
  
};

function Bear(name) {
  this.name = name; 
}

Bear.prototype = {
  constructor: Bear, 
  
};

function Animal() { }

Animal.prototype = {
  constructor: Animal,
  eat: function() {
    console.log("nom nom nom");
  }
};
```

<div id="id-19"/>

### Inherit Behaviors from a Supertype

In previous challenge, you created a supertype called Animal that defined behaviors shared by all animals:
```
function Animal() {}
Animal.prototype.eat = function() {
    console.log("nom nom nom");
}
```
This and the next challenge will cover hwo to reuse Animal's methods inside Bird and Dog without defining them again. It uses a technique called inheritance.

This challenge covers the first step: make an instance of the supertype (or parent).
You already know onw way to create an instance of Animal using new operator:

```
let animal = new Animal();
```
There are some disadvantages when using this syntax for inheritance, which are too complex for the scope of this challenge.
Instead, here's an alternative approach without those disadvantages:

```
let animal = Object.create(Animal.prototype);
```

Object.create(obj) creates a new object, and sets obj as the new object's prototype. Recall that the prototype is like the "recipe" for creating an object. By setting the prototype of animal to be Animal's prototype, you are effectively giving the animal instance the same "recipe" as any other instance of Animal.

```
animal.eat(); // prints "nom nom nom"
animal instanceof Animal; // true
```

Use Object.create to make two instances of Animal named duck and beagle.

```
function Animal() { }

Animal.prototype = {
  constructor: Animal, 
  eat: function() {
    console.log("nom nom nom");
  }
};

// Add your code below this line

let duck = Object.create(Animal.prototype); // Change this line
let beagle = Object.create(Animal.prototype); // Change this line

duck.eat(); // Should print "nom nom nom"
beagle.eat(); // Should print "nom nom nom" 
```

<div id="id-20"/>

### Set the Child's Prototype to an Instance of the Parent

Above we saw the first step for inheriting behavior from the supertype (or parent) Animal:making a new instance of Animal

This challenge covers the next step:set the prototype of the subtype (or child)-in this case, Bird- to be an instance of Animal.

```
Bird.prototype = Object.create(Animal.prototype);
```

Remember that the prototype is like the "recipe" for creating an object. In a way, the recipe for Bird now includes all the key "ingredients" from Animal.

```
let duck = new Bird("Donald");
duck.eat(); // prints "nom nom nom"
```
duck inherits all of Animal's properties, including eat method.

Modify the code so that instances of Dog inherit from Animal.

```
function Animal() { }

Animal.prototype = {
  constructor: Animal,
  eat: function() {
    console.log("nom nom nom");
  }
};

function Dog() { }

// Add your code below this line
Dog.prototype = Object.create(Animal.prototype);


let beagle = new Dog();
beagle.eat();  // Should print "nom nom nom"
```

<div id="id-21"/>

### Reset an Inherited Constructor Property

When an object inherits its prototype from another object, it also inherits the supertype's constructor property. 
Here's an example:
```
function Bird() {}
Bird.prototype = Object.create(Animal.prototype);
let duck = new Bird();
duck.constructor    // function Animal() {...}
```
But duck and all instances of Bird should show that they were constructed by Bird and not Animal. To do so, you can manually set Bird's constructor property to the Bird object:

```
Bird.prototype.constructor = Bird;
duck.constructor // function Bird() {...}
```

Fix the code so duck.constructor and beagle.constructor return their respective constructors.

```
function Animal() { }
function Bird() { }
function Dog() { }

Bird.prototype = Object.create(Animal.prototype);
Dog.prototype = Object.create(Animal.prototype);

// Add your code below this line
Bird.prototype.constructor = Bird;
Dog.prototype.constructor = Dog;


let duck = new Bird();
let beagle = new Dog();
```

<div id="id-22"/>

### Add Methods After Inheritance

A constructor function that inherits its prototype object from a supertype constructor function can still have its own methods in addition to inherited methods.

For example, Bird is a constructor that inherits its prototype from Animal:
```
function Animal() { }
Animal.prototype.eat = function() {
    console.log("nom nom nom");
};

function Bird() { }
Bird.prototype = Object.create(Animal.prototype);
Bird.prototype.constructor = Bird;
```

In addition to what is inherited from Animal, you want to  add behavior that is unique to Bird objects. Here, Bird will get a fly() function. Functions are added to Bird's prototype the same way as any constructor function:

```
Bird.prototype.fly = function() {
    console.log("I'm flying!");
};
```

Now instances of Bird will have both eat() and fly() methods:
```
let duck = new Bird();
duck.eat(); // prints "nom nom nom"
duck.fly(); // prints "I'm flying!"
```

Add all necessary code so the Dog object inherits from Animal and the Dog's prototype constructor is set to Dog. Then add a bark() method to the Dog object so that beagle can both eat() and bark(). The bark() method should print "Woof!" to the console.

```
function Animal() { }
Animal.prototype.eat = function() { console.log("nom nom nom"); };

function Dog() { }

// Add your code below this line
Dog.prototype = Object.create(Animal.prototype);
Dog.prototype.constructor = Dog;
Dog.prototype.bark = function() { console.log("Woof!"); };



// Add your code above this line

let beagle = new Dog();

beagle.eat(); // Should print "nom nom nom"
beagle.bark(); // Should print "Woof!"
```

<div id="id-23"/>

### Override Inherited Methods

In previous lessons, you learned that an object can inherit its behavior(methods) from another object bu cloning its prototype object:

```
ChildObject.prototype = Object.create(ParentObject.prototype);
```

Then the ChildObject received its own methods by chaining them onto its prototype:

```
ChildObject.prototype.methodName = function() {...};
```

It's possible to override an inherited method. It's done the same way- by adding a method to ChildObject.prototype using the same method name as the one to override:

Here's an example of Bird overriding the eat() method inherited from Animal:

```
function Animal() { }
Animal.prototype.eat = function() {
  return "nom nom nom";
};
function Bird() { }

// Inherit all methods from Animal
Bird.prototype = Object.create(Animal.prototype);

// Bird.eat() overrides Animal.eat()
Bird.prototype.eat = function() {
  return "peck peck peck";
};

```

If you have an instance let duck = new Bird(); and you call duck.eat(), this is how JavaScript looks for the method on duck's prototype chain:

1. duck => Is eat() defined here? No.
2. Bird => Is eat() defined here? => Yes. Execute it and stop searching
3. Animal => eat() is also defined, but JavaScript stopped searching before reaching this level.
4. Object => JavaScript stopped searching before reaching this level

Override the fly() method for Penguin so that it returns "Alas, this is a flightless bird."

```
function Bird() { }

Bird.prototype.fly = function() { return "I am flying!"; };

function Penguin() { }
Penguin.prototype = Object.create(Bird.prototype);
Penguin.prototype.constructor = Penguin;

// Add your code below this line
Penguin.prototype.fly = function() {
    return "Alas, this is a flightless bird.";
};


// Add your code above this line

let penguin = new Penguin();
console.log(penguin.fly());
```

<div id="id-24"/>

### Use a Mixin to Add Common Behavior Between Unrelated Objects

As you have seen, behavior is shared through inheritance. However, there is cases when inheritance is not the best solution. Inheritance does not work well for unrelated objects like Bird and Airplane. They can both fly, but a Bird is not a type of Airplane and vice versa.

For unrelated objects, it's better to mixins. A mixin allows other objects to use a collection of functions.

```
let flyMixin = function(obj) {
    obj.fly = function() {
        console.log("Flying, wooosh!");
    }
};
```
The flyMixin takes any object and gives it the fly method.

```

let bird = {
  name: "Donald",
  numLegs: 2
};

let plane = {
  model: "777",
  numPassengers: 524
};

flyMixin(bird);
flyMixin(plane);

```
Here bird and plane are passed into flyMixin, which then assigns the fly function to each object. Now bird and plane can both fly:

```
bird.fly(); // prints "Flying, wooosh!"
plane.fly(); // prints "Flying, wooosh!"
```

Note how the mixin allows for the same fly method to be reused by unrelated objects bird and plane.

Create a mixin named glideMixin that defines a method named glide. Then use the glideMixin to give both bird and boat the ability to glide.

```
let bird = {
  name: "Donald",
  numLegs: 2
};

let boat = {
  name: "Warrior",
  type: "race-boat"
};

// Add your code below this line
let glideMixin = function(obj) {
    obj.glide = function() {
        console.log("Gliding");
    }
};

glideMixin(bird);
glideMixin(boat);
```

<div id="id-25"/>

### Use Closure to Protect Properties Within an Object from Being Modified Externally

In the previous challenge, bird had a public property name. It is considered public because it can be accessed and changed outside of bird's definition.

```
bird.name = "Duffy";
```
Therefore, any part of your code can easily change the name of bird to any value. Think about things like passwords and bank accounts being easily changeable by any part of your codebase. That could cause a lot of issues.

The simplest way to make properties private is by creating a variable within the constructor function. This changes the scope of that variable to be within the constructor function versus available globally. This way, the property can only be accessed and changed by methods also within the constructor function.

```
function Bird() {
    let hatchedEgg = 10;    // private property

    this.getHatchedEggCount = function() {  // publicly available method that a bird object can use
        return hatchedEgg;
    };
}
let ducky = newBird();
ducky.getHatchedEggCount(); // returns 10
```
Here getHatchedEggCount is a privileged method, because it has access to the private variable hatchedEgg. This is possible because hatchedEgg is declared in the same context as getHatchedEggCount. In JavaScript, a function always has access to the context in which it was created. This is called closure.

Change how weight is declared in the Bird function so it is a private variable. Then, create a method getWeight that returns the value of weight.

```
function Bird() {
  let weight = 15;

  this.getWeight = function() {
    return weight;
  } 
  
}

```

<div id="id-26"/>

### Understand the Immediately Invoked Function Expression (IIFE)

A common pattern inJavaScript is to execute a function as soon as it is declared:
```
(function () {
    console.log("Chirp, chirp!");
}) (); // this is an anonymous function expression that executes right away
// Outputs "Chirp, chirp!" immediately
```
Note that the function has no name and is not stored in a variable. The two parentheses() at the end of the the function expression cause it to be immediately executed or invoked. This pattern is known as an **immediately invoked function expression** or **IIFE**.

Rewrite the function makeNest and remove its call so instead it's an anonymous immediately invoked function expression (IIFE).

```
function makeNest() {
  console.log("A cozy nest is ready");
}

makeNest(); 

-----------------------------------------
(function () {
  console.log("A cozy nest is ready");
}) ();

```

<div id="id-27"/>

### Use an IIFE to Create a Module

An immediately invoked function expression (IIFE) is often used to group related functionality into a single object or module. For example, an earlier challenge defined two mixins:

```
function glideMixin(obj) {
    obj.glide = function() {
        console.log("Gliding on the water");
    };
}
function flyMixin(obj) {
    obj.fly = function() {
        console.log("Flying, wooosh!");
    };
}
```
We can group these mixins into a module as follows:
```
let motionModule = (function () {
    return {
        glideMixin: function (obj) {
            obj.glide = function() {
                console.log("Gliding on the water");
            };
        },
        flyMixin: function(obj) {
            obj.fly = function() {
                console.log("Flying, wooosh!");
            };
        }
    }
}) ();  // The two parentheses cause the function to be immediately invoked
```

Note that you have an immediately invoked function expression (IIFE) that returns an object motionModule. This returned object contains all of the mixin behavior as properties of the object.

The advantage of the module pattern is that all of the motion behaviors can be packaged into a single object that can then be used by other parts of your code. Here is an example using it:

```
motionModule.glideMixin(duck);
duck.glide();
```
Create a module named funModule to wrap the two mixins isCuteMixin and singMixin. funModule should return an object.

```
let isCuteMixin = function(obj) {
  obj.isCute = function() {
    return true;
  };
};
let singMixin = function(obj) {
  obj.sing = function() {
    console.log("Singing to an awesome tune");
  };
};


____________________________________________________

let funModule = (function () {
  return {
    isCuteMixin: function(obj) {
      obj.isCute = function() {
        return true;
      };
    },
    singMixin: function(obj) {
      obj.sing = function() {
        console.log("Singing to an awesome tune");
      };
    }
  }
}) ();

```

---

<div id="functional-programming"/>

# Functional Programming

Table of Contents
1. [Introduction to the Functional Programming Challenges](#1a)
2. [Learn About Functional Programming](#2a)
3. [Understand Functional Programming Terminology](#3a)
4. [Understand the Hazards of Using Imperative Code](#4a)
5. [Avoid Mutations and Side Effects Using Functional Programming](#5a)
6. [Pass Arguments to Avoid External Dependence in a Function](#6a)
7. [Refactor Global Variables Out of Functions](#7a)
8. [Use the map Method to extract Data from an Array](#8)
9. [Implement map on a Prototype](#9a)
10. [Use the filter Method to Extract Data from an Array](#10a)
11. [Implement the filter Method on a Prototype](#11a)
12. [Return Part of an Array Using the slice Method](#12a)
13. [Remove Elements from an Array Using slice Instead of splice](#13a)
14. [Combine Two Arrays Using the concat Method](#14)
15. [Add Elements to the End of an Array Using concat Instead of push](#15a)
16. [Use the reduce Method to Analyze Data](#16a)
17. [Sort an Array Alphabetically using the sort Method](#17a)
18. [Return a Sorted Array Without Changing the Original Array](#18a)
19. [Split a String into an Array Using the split Method](#19a)
20. [Combine an Array into a String Using the join Method](#20a)
21. [Apply Functional Programming to Convert Strings to URL Slugs](#21a)
22. [Use the every Method to Check that Every Element in an Array Meets a Criteria](#22a)
23. [Use the some Method to Check that Any Elements in an Array Meet a Criteria](#23a)
24. [Introduction to Currying and Partial Application](#24a)
25. [Appendix Notes](#25a)

<div id="1a"/>

### Introduction to the Functional Programming Challenges

Functional programming is an approach to software development based around the evaluation of functions. Like mathematics, functions in programming map input to output to produce a result. You can combine basic functions in many ways to build more and more complex programs.

Functional programming follows a few core principles:

* Functions are independent from the state of the program of global variables. They only depend on the arguments passed into them to make a calculation.
* Functions try to limit any changes to the state of the program and avoid changes to the global objects holding data.
* Functions have minimal side effects in the program.

The functional programming software development approach breaks a program into small, testable parts. This section covers basic functional programming principles in JavaScript.

<div id="2a"/>

### Learn About Functional Programming

Functional programming is a style of programming where solutions are simple, isolated functions, without any side effects outside of the function scope.

INPUT -> PROCESS -> OUTPUT

Functional programming is about:

1) Isolated functions - there is no dependence on the state of the program, which includes global variables that are subject to change

2) Pure functions - the same input always gives the same output

3) Functions with limited side effects - any changes, or mutations, to the state of the program outside the function are carefully controlled
_______________________________________________________________
In the code editor, the prepareTea and getTea functions are already defined for you. Call the getTea function to get 40 cups of tea for the team, and store them in the tea4TeamFCC variable.

```
/**
 * A long process to prepare tea.
 * @return {string} A cup of tea.
 **/
const prepareTea = () => 'greenTea';
 
/**
 * Get given number of cups of tea.
 * @param {number} numOfCups Number of required cups of tea.
 * @return {Array<string>} Given amount of tea cups.
 **/
const getTea = (numOfCups) => {
  const teaCups = [];
  
  for(let cups = 1; cups <= numOfCups; cups += 1) {
    const teaCup = prepareTea();
    teaCups.push(teaCup);
  }
 
  return teaCups;
};
 
// Add your code below this line
 
// const tea4TeamFCC = null; // :(
   const tea4TeamFCC = getTea(40);
 
// Add your code above this line
 
console.log(tea4TeamFCC);
```

<div id="3a"/>

### Understand Functional Programming Terminology

The team wants two types of tea: green tea and black tea. 
With that info, we'll need to revisit the getTea function from last challenge to handle various tea requests. We can modify getTea to accept a function as a parameter to be able to change the type of tea it prepares. This makes getTea more flexible, and gives the programmer more control when client requests change.

But first let's cover some functional terminology:

Callbacks are the functions that are slipped or passed into another function to decide the invocation of that function. You may have seen them passed to other methods, for example in filter, the callback function tells JavaScript the criteria for how to filter an array. 

Functions that can be assigned to a variable, passed into another function, or returned from another function just like any other normal value, are called _first class_ functions.

These functions that take a function as an argument, or return a function as a return value are called higher order functions.

When the functions are passed in to another function or returned from another function, then those functions which gets passed in or returned can be called a **lambda**
___________________________________________________________________
Prepare 27 cups of green tea and 13 cups of black tea and store them in tea4GreenTeamFCC and tea4BlackTeamFCC variables, respectively. Note that the getTea function has been modified so it now takes a function as the first argument.

Note: The data (the number of cups of tea) is supplied as the last argument. We'll discuss this more in later lessons.

```
/**
* A long process to prepare green tea.
* @return {string} A cup of green tea.
**/
const prepareGreenTea = [] => 'greenTea';

/**
* A long process to prepare black tea.
* @return {string} A cup of black tea.
**/
const prepareBlackTea = () => 'blackTea';

/**
 * Get given number of cups of tea.
 * @param {function():string} prepareTea The type of tea preparing function.
 * @param {number} numOfCups Number of required cups of tea.
 * @return {Array<string>} Given amount of tea cups.
 **/
const getTea = (prepareTea, numOfCups) => {
  const teaCups = [];

  for(let cups = 1; cups <= numOfCups; cups += 1) {
    const teaCup = prepareTea();
    teaCups.push(teaCup);
  }

  return teaCups;
};

// Add your code below this line

//const tea4GreenTeamFCC = null; // :(
//const tea4BlackTeamFCC = null; // :(
const tea4GreenTeamFCC = getTea(prepareGreenTea, 27); // :(
const tea4BlackTeamFCC = getTea(prepareBlackTea, 13); // :(

// Add your code above this line

console.log(
  tea4GreenTeamFCC,
  tea4BlackTeamFCC
);

```

<div id="4a"/>

### Understand the Hazards of Using Imperative Code

Functional programming is a good habit. It keeps your code easy to manage, and saves you from sneaky bugs. But before we get there, let's look at an imperative approach to programming to highlight where you may have issues.

In English (and many other languages), the imperative tense is used to give commands. Similarly, an imperative style in programming is one that gives the computer a set of statements to perform a task.

Often the statements change the state of the program, like updating global variables. A classic example of writing a for loop that gives exact directions to iterate over the indices of an array.

In contrast, functional programming is a form of declarative programming. You tell the computer what you want done by calling a method or function.

JavaScript offers many predefined methods that handle common tasks so you don't need to write out how the computer should perform them. For example, instead of using the for loop mentioned above, you could call the map method which handles the details of iterating over an array. This helps to avoid semantic errors, like the "Off By One Errors" that were covered in the Debugging section.

Consider the scenario: you are browsing the web in your browser. and want to track the tabs you have opened. The titles of each open site in each Window object is held in an array. After working in the browser (opening new tabs, merging windows, and closing tabs), you want to print the tabs that are still open. Closed tabs are removed from the array and new tabs (for simplicity) get added to the end of it.

The code editor shows an implementation of this functionality with functions for tapOpen(), tabClose(), and join().
The array tabs is part of the Window object that stores the name of the open pages.

Instructions

Run the code in the editor. It's using a method that has side effects in the program, causing incorrect output. The final list of open tabs should be ['FB', 'Gitter', 'Reddit', 'Twitter', 'Medium', 'new tab', 'Netflix', 'YouTube', 'Vine', 'GMail', 'Work mail', 'Docs', 'freeCodeCamp', 'new tab'] but the output will be slightly different. 

Work through the code and see if you can figure out the problem, then advance to the next challenge to learn more

```
// tabs is an array if titles of each site open within the window
var Window = function(tabs) {
    this.tabs =tabs;    // we keep a record of the array inside the object
};

// When you join two windows into one window
Window.prototype.join = function (otherWindow) {
    this.tabs = this.tabs.concat(otherWindow.tabs);
    return this;
};

// When you open a new tab at the end
Window.prototype.tabOpen = function (tab) {
    this.tabs.push('new tab');  // let's open a new tab for now
    return this;
};

// When you close a tb
Window.prototype.tabClose = function (index) {
    var tabsBeforeIndex = this.tabs.splice(0, index);   // get the tabs before the tab
    var tabsAfterIndex = this.tabs.splice(index);   // get the tabs after the tab

    this.tabs = tabsBeforeIndex.concat(tabsAfterIndex); // join them together
    return this;
};

// Let's create three browser windows
var workWindow = new Window(['GMail', 'Inbox', 'Work mail', 'Docs', 'freeCodeCamp']);   // Your mailbox,
// drive, and other work sites.
var socialWindow = new Window(['FB', 'Gitter', 'Reddit', 'Twitter', 'Medium']); // Social sites
var videoWindow = new Window(['Netflix', 'YouTube', 'Vimeo', 'Vine']);  // Entertainment sites

// Now perform the tab opening, closing, and other operations
var finalTabs = socialWindow
                    .tabOpen()  // Open a new tab for cat memes
                    .join(videoWindow.tabClose(2))  // Close third tab in vide window, and join
                    .join(workWindow.tabClose(1).tabOpen());
console.log(finalTabs.tabs);
```

<div id="5a"/>

### Avoid Mutations and Side Effects Using Functional Programming

If you haven't already figured it out, the issue in the previous challenge was with the splice call in the tabClose() function. Unfortunately, splice changes the original array it is called on, so the second call to it used a modified array, and gave unexpected results.

This is a small example of a much larger pattern - you call a function on a variable, array, or an object, and the function changes the variable or something in the object.

One of the core principle of functional programming is to not change things. Changes lead to bugs. It's easier to prevent bugs knowing that your functions don't change anything, including the function arguments or any global variable. 

The previous example didn't have any complicated operations but the splice method changed the original array, and resulted in a bug.

Recall that in functional programming, changing or altering things is called mutation, and the outcome is called a side effect. A function, ideally, should be a pure function, meaning that it does not cause any side effects.

Let's try to master this discipline and not alter any variables or object in our code.
____________________________________________________________________________________
Fill in the code for the function incrementor so it returns the value of the global variable fixedValue increased by one.

```
// the global variable
var fixedValue = 4;

function incrementor () {
  // Add your code below this line
  
  
  // Add your code above this line
}

var newValue = incrementor(); // Should equal 5
console.log(fixedValue); // Should print 4
```

<div id="6a"/>

### Pass Arguments to Avoid External Dependence in a Function

The last challenge was a step closer to functional programming principles, but there is still something missing.

We didn't alter the global variable value, but the function incrementor would not work without the global variable fixedValue being there.

Another principle of functional programming is to always declare your dependencies explicitly. This means if a function depends on a variable or object being present, then pass that variable or object directly into the function as an argument.

There are several good consequences from this principle. The function is easier to test, you know exactly what input it takes, and it won't depend on anything else in your program.

This can give you more confidence when you alter, remove, or add new code. You would know what you can or cannot change and you can see where the potential traps are.

Finally, the function would always produce the same output for the same set of inputs, no matter what part of the code executes it.

Let's update the incrementor function to clearly declare its dependencies.

Write the incrementor function so it takes an argument, and then increases the value by one.

```
// the global variable
var fixedValue = 4;

// Add your code below this line
function incrementor (fixedValue) {
  return fixedValue + 1;
  
  // Add your code above this line
}

var newValue = incrementor(fixedValue); // Should equal 5
console.log(fixedValue); // Should print 4
```

<div id="7a"/>

### Refactor Global Variables Out of Functions

So, far we have seen two distinct principles for functional programming.

1) Don't alter a variable or object - create new variables and objects and return them if need be from a function

2) Declare function arguments - any computation inside a function depends only on the arguments, and not on any global object or variable.

Adding one to a number is not very exciting, but we can apply these principles when working with arrays or more complex objects.
_____________________________________________________________________________________
Refactor (rewrite) the code so the global array bookList is not changed inside either function. The add function should add the given bookName to the end of an array. The remove function should remove the given bookName from an array. Both function should return an array, and any new parameters should be added before the bookName one.

```
// the global variable
var bookList = ["The Hound of the Baskervilles", "On The Electrodynamics of Moving Bodies", "Philosophiæ Naturalis Principia Mathematica", "Disquisitiones Arithmeticae"];

/* This function should add a book to the list and return the list */
// New parameters should come before the bookName one

// Add your code below this line
function add (list, bookName) { 
  return [...list, bookName]; // use the spread operator to put the list inside and array and the add the bookName as the last element.
}

/* This function should remove a book from the list and return the list */
// New parameters should come before the bookName one

// Add your code below this line
function remove (list, bookName) {  // takes to parameter
  if (list.indexOf(bookName) >= 0) {  // if the indexOf in list called bookName is greater than or equal to 0
    return list.filter((item) => item !== bookName);  // then filter through the list and return any item that is not === bookName so that it is removed from the list.
  }
}


var newBookList = add(bookList, 'A Brief History of Time');
var newerBookList = remove(bookList, 'On The Electrodynamics of Moving Bodies');
var newestBookList = remove(add(bookList, 'A Brief History of Time'), 'On The Electrodynamics of Moving Bodies');

console.log(bookList);
```

<div id="8a"/>

### Use the map Method to extract Data from an Array

So far we have learned to use pure functions to avoid side effects in a program. Also, we have seen the value in having a function only depend on its t arguments.

This is only the beginning. As its name suggests, functional programming is centered around a theory of functions.

It would make sense to be able to pass them as arguments to other functions, and return a function from another function. Functions are considered First Class Objects in JavaScript, which means they can be used like any other object. They can be saved in variables, stored in an object, or passed as function arguments.

Let's start with some simple array functions, which are methods on the array object prototype. In this exercise we are looking at Array.prototype.map(), or more simply map.'

Remember that the map method is a way ot iterate over each item in an array. It creates a new array (without changing the original one) after applying a callback function to every element. 
_________________________________________________________________
The watchList array holds objects with information on several movies. Use map to pull the title and rating from watchList and save the new array in the rating variable. The code in the editor currently uses a for loop to do this, replace the loop functionality with your map expression.

```
// the global variable
var watchList = [
    {  
      "Title": "Inception",
      "Year": "2010",
      "Rated": "PG-13",
      "Released": "16 Jul 2010",
      "Runtime": "148 min",
      "Genre": "Action, Adventure, Crime",
      "Director": "Christopher Nolan",
      "Writer": "Christopher Nolan",
      "Actors": "Leonardo DiCaprio, Joseph Gordon-Levitt, Ellen Page, Tom Hardy",
      "Plot": "A thief, who steals corporate secrets through use of dream-sharing technology, is given the inverse task of planting an idea into the mind of a CEO.",
      "Language": "English, Japanese, French",
      "Country": "USA, UK",
      "Awards": "Won 4 Oscars. Another 143 wins & 198 nominations.",
      "Poster": "http://ia.media-imdb.com/images/M/MV5BMjAxMzY3NjcxNF5BMl5BanBnXkFtZTcwNTI5OTM0Mw@@._V1_SX300.jpg",
      "Metascore": "74",
      "imdbRating": "8.8",
      "imdbVotes": "1,446,708",
      "imdbID": "tt1375666",
      "Type": "movie",
      "Response": "True"
   },
   {  
      "Title": "Interstellar",
      "Year": "2014",
      "Rated": "PG-13",
      "Released": "07 Nov 2014",
      "Runtime": "169 min",
      "Genre": "Adventure, Drama, Sci-Fi",
      "Director": "Christopher Nolan",
      "Writer": "Jonathan Nolan, Christopher Nolan",
      "Actors": "Ellen Burstyn, Matthew McConaughey, Mackenzie Foy, John Lithgow",
      "Plot": "A team of explorers travel through a wormhole in space in an attempt to ensure humanity's survival.",
      "Language": "English",
      "Country": "USA, UK",
      "Awards": "Won 1 Oscar. Another 39 wins & 132 nominations.",
      "Poster": "http://ia.media-imdb.com/images/M/MV5BMjIxNTU4MzY4MF5BMl5BanBnXkFtZTgwMzM4ODI3MjE@._V1_SX300.jpg",
      "Metascore": "74",
      "imdbRating": "8.6",
      "imdbVotes": "910,366",
      "imdbID": "tt0816692",
      "Type": "movie",
      "Response": "True"
   },
   {
      "Title": "The Dark Knight",
      "Year": "2008",
      "Rated": "PG-13",
      "Released": "18 Jul 2008",
      "Runtime": "152 min",
      "Genre": "Action, Adventure, Crime",
      "Director": "Christopher Nolan",
      "Writer": "Jonathan Nolan (screenplay), Christopher Nolan (screenplay), Christopher Nolan (story), David S. Goyer (story), Bob Kane (characters)",
      "Actors": "Christian Bale, Heath Ledger, Aaron Eckhart, Michael Caine",
      "Plot": "When the menace known as the Joker wreaks havoc and chaos on the people of Gotham, the caped crusader must come to terms with one of the greatest psychological tests of his ability to fight injustice.",
      "Language": "English, Mandarin",
      "Country": "USA, UK",
      "Awards": "Won 2 Oscars. Another 146 wins & 142 nominations.",
      "Poster": "http://ia.media-imdb.com/images/M/MV5BMTMxNTMwODM0NF5BMl5BanBnXkFtZTcwODAyMTk2Mw@@._V1_SX300.jpg",
      "Metascore": "82",
      "imdbRating": "9.0",
      "imdbVotes": "1,652,832",
      "imdbID": "tt0468569",
      "Type": "movie",
      "Response": "True"
   },
   {  
      "Title": "Batman Begins",
      "Year": "2005",
      "Rated": "PG-13",
      "Released": "15 Jun 2005",
      "Runtime": "140 min",
      "Genre": "Action, Adventure",
      "Director": "Christopher Nolan",
      "Writer": "Bob Kane (characters), David S. Goyer (story), Christopher Nolan (screenplay), David S. Goyer (screenplay)",
      "Actors": "Christian Bale, Michael Caine, Liam Neeson, Katie Holmes",
      "Plot": "After training with his mentor, Batman begins his fight to free crime-ridden Gotham City from the corruption that Scarecrow and the League of Shadows have cast upon it.",
      "Language": "English, Urdu, Mandarin",
      "Country": "USA, UK",
      "Awards": "Nominated for 1 Oscar. Another 15 wins & 66 nominations.",
      "Poster": "http://ia.media-imdb.com/images/M/MV5BNTM3OTc0MzM2OV5BMl5BanBnXkFtZTYwNzUwMTI3._V1_SX300.jpg",
      "Metascore": "70",
      "imdbRating": "8.3",
      "imdbVotes": "972,584",
      "imdbID": "tt0372784",
      "Type": "movie",
      "Response": "True"
   },
   {
      "Title": "Avatar",
      "Year": "2009",
      "Rated": "PG-13",
      "Released": "18 Dec 2009",
      "Runtime": "162 min",
      "Genre": "Action, Adventure, Fantasy",
      "Director": "James Cameron",
      "Writer": "James Cameron",
      "Actors": "Sam Worthington, Zoe Saldana, Sigourney Weaver, Stephen Lang",
      "Plot": "A paraplegic marine dispatched to the moon Pandora on a unique mission becomes torn between following his orders and protecting the world he feels is his home.",
      "Language": "English, Spanish",
      "Country": "USA, UK",
      "Awards": "Won 3 Oscars. Another 80 wins & 121 nominations.",
      "Poster": "http://ia.media-imdb.com/images/M/MV5BMTYwOTEwNjAzMl5BMl5BanBnXkFtZTcwODc5MTUwMw@@._V1_SX300.jpg",
      "Metascore": "83",
      "imdbRating": "7.9",
      "imdbVotes": "876,575",
      "imdbID": "tt0499549",
      "Type": "movie",
      "Response": "True"
   }
];

// Add your code below this line

// var rating = [];
// for(var i=0; i < watchList.length; i++){
// rating.push({title: watchList[i]["Title"],  rating: watchList[i]["imdbRating"]});
// }

let ratings = watchList.map(function(movie) {
    return ({title: movie.Title,  rating: movie.imdbRating});
});

// Add your code above this line

console.log(ratings); 
```

<div id="9a"/>

### Implement map on a Prototype

As you have seen from applying Array.prototype.map(), or simply map() earlier, the map method returns an array of the same length as the one it was called on. It also doesn't alter the original array, as long as its callback function doesn't. 

In other words, map is a pure function, and its output depends solely on its inputs. Plus, it takes another function as its argument.

It would teach us a lot abut map to try to implement a version of it that behaves exactly like the Array.prototype.map() with a for loop or Array.prototype.forEach()

Note: A pure function is allowed to alter local variables defined within its scope, although, it's preferable to avoid that as well.
___________________________________________________________________________
Write your own Array.prototype.myMap(), which should behave exactly like Array.prototype.map(). You may use a for loop or the forEach method.

```
// the global Array
var s = [23, 65, 98, 5];

Array.prototype.myMap = function(callback){
  var newArray = [];
  // Add your code below this line
  for (var i = 0; i < s.length; i++) {
    newArray.push(s[i] * 2);
  }
  
  // Add your code above this line
  return newArray;

};

var new_s = s.myMap(function(item){
  return item * 2;
});
```

<div id="10a"/>

### Use the filter Method to Extract Data from an Array

Another useful array function is Array.prototype.filter(), or simply filter(). The filter method returns a new array which is at most as long as the original array, but usually has fewer items.

Filter doesn't alter the original array, just like map. It takes a callback function that applies logic inside the callback on each element of the array. If an element returns true based on the criteria in the callback function. then it is included in the new array.
____________________________________________________________________
The variable watchList holds an array of objects with information on several movies. Use a combination of filter and map to return a new array of objects with only title and rating keys, but where imdbRating is greater than or equal to 8.0. Note that the rating values are saved as strings in the object and you may want to convert them into numbers to perform mathematical operations on them.


<div id="11a"/>

### Implement the filter Method on a Prototype

It would teach us a lot about the filter method if we try to implement a version of it that behaves exactly like Array.prototype.filter(). It can use either a for loop or Array.prototype.forEach().

Note: A pure function is allowed to alter local variables defined within its scope, although, it's preferable to avoid that as well.
_________________________________________________________________________
Write your own Array.prototype.myFilter(), which should behave exactly like Array.prototype.filter(). You may use a for loop or the Array.prototype.forEach() method.

```
// the global Array
var s = [23, 65, 98, 5];
 
Array.prototype.myFilter = function(callback){
  var newArray = [];
  // Add your code below this line
  this.forEach(function(elem) {
    if (callback(elem) == true) {
      newArray.push(elem);
    }
  });
  // Add your code above this line
  return newArray;
 
};
 
var new_s = s.myFilter(function(item){
  return item % 2 === 1;
});

```

<div id="12a"/>

### Return Part of an Array Using the slice Method

The slice method returns a copy of certain elements of an array. It can take two arguments, the first gives the index of where to begin the slice, the second is the index for where to end the slice (and it's non-inclusive). If the arguments are not provided, the default is to start at the beginning of the array through the end, which is an easy way to make a copy of the entire array. The slice method does not mutate the original array, but returns anew one.

Here's an example:
```
var arr = ["Cat", "Dog", "Tiger", "Zebra"];
var newArray = arr.slice(1, 3);
// Sets newArray to ["Dog", "Tiger"]
```
______________________________________________________________
Use the slice method in the sliceArray function to return part of the anim array given the provided beginSlice and endSlice 
indices. The function should return an array

```
function sliceArray(anim, beginSlice, endSlice) {
  // Add your code below this line
  return anim.slice(beginSlice, endSlice);
  
  // Add your code above this line
}
var inputAnim = ["Cat", "Dog", "Tiger", "Zebra", "Ant"];
sliceArray(inputAnim, 1, 3);
```

<div id="13a"/>

### Remove Elements from an Array Using slice Instead of splice

A common pattern while working with arrays is when you want to remove items and keep the rest of the array. JavaScript offers the splice method for this, which takes arguments for the index of where to start removing items, then the number of items to remove. If the second argument is not provided, the default is to remove items through the end. However, the splice method mutates the original array it is called on. 
Here's an example:

```
var cities = ["Chicago", "Dehli", "Islamabad", "London", "Berlin"];
cities.splice(3, 1);  // Returns "London and deletes it from the cities array
// cities is now ["Chicago", "Delhi", "Islamabad", "Berlin"]
```

As we saw in the last challenge, the slice method does not mutate the original array, but returns a new one which can be saved into a variable. Recall that the slice method takes two arguments for the indices to begin and end the slice (the end is non-inclusive), and returns those items in a new array. Using the slice method instead of splice helps to avoid any array-mutating side effects.
____________________________________________________________________________________________
Rewrite the function nonMutatingSplice by using slice instead of splice. It should limit the provided cities array to a length of 3, and return a new array with only the first three items.

Do not mutate the original array provided to the function.

```
function nonMutatingSplice(cities) {
  // Add your code below this line
  return cities.slice(0, 3);
  
  // Add your code above this line
}
var inputCities = ["Chicago", "Delhi", "Islamabad", "London", "Berlin"];
nonMutatingSplice(inputCities);
```

<div id="14a"/>

### Combine Two Arrays Using the concat Method

_Concatenation_ means to join items end to end. JavaScript offers the concat method for both strings and arrays that work in the same way. For arrays, the method is called on one, then another array is provided as the argument to concat, which is added to the end of the first array. It returns a new array and does not mutate either of the original arrays. Here's an example: 

```
[1, 2, 3].concat([4, 5, 6]);
// Returns a new array [1, 2, 3, 4, 5, 6]
```
_____________________________________________________________________
Use the concat method in the nonMutatingConcat function to concatenate attach to the end of original. The function should return the concatenated array.

```
function nonMutatingConcat(original, attach) {
  // Add your code below this line
  return original.concat(attach);
  
  // Add your code above this line
}
var first = [1, 2, 3];
var second = [4, 5];
nonMutatingConcat(first, second);
```

<div id="15a"/>

### Add Elements to the End of an Array Using concat Instead of push

Functional programming is all about creating and using non-mutating functions.

The last challenge introduced the concat method as a way to combine arrays into a new one without mutating the original arrays. Compare concat to the push method. Push adds an item to the end of the same array it is called on, which mutates that array. Here's an example:

```
var arr = [1, 2, 3];
arr.push([4, 5, 6]);
// arr is changed to [1, 2, 3, [4, 5, 6]]
// Not the functional programming way
```

Concat offers a way to add new items to the end of an array without any mutating side effects.
_________________________________________________________________________________
Change the nonMutatingPush function so it uses concat to add newItem to the end of original instead of push. The function should return an array.

```
function nonMutatingPush(original, newItem) {
  // Add your code below this line
  // return original.push(newItem);
  return original.concat(newItem);
  
  // Add your code above this line
}
var first = [1, 2, 3];
var second = [4, 5];
nonMutatingPush(first, second);
```

<div id="16a"/>

### Use the reduce Method to Analyze Data 

Array.prototype.reduce(), or simply reduce(), is the most general of all array operations in JavaScript. You can solve almost any array processing problem using the reduce method. 

This is not the case with the filter and map methods since they do not allow interaction between two different elements of the array. For example, if you want to compare elements of the array, or add them together, filter or map could not process that . 

The reduce method allows for more general forms of array processing, and it's possible to show that both filter and map can be derived as a special application of reduce.

However, before we get there, let's practice using reduce first.
__________________________________________________________________________________________
The variable watchList holds an array of objects with information on several movies. Use reduce to find the average IMDB rating of the movies directed by Christopher Nolan. Recall from prior challenges how to filter data and map over it to pull what you need. You may need to create other variables, but save the final average into the variable averageRating. Note that the rating values are saved as strings in the object and need to be converted into numbers before they are used in any mathematical operations.


<div id="17a"/>

### Sort an Array Alphabetically using the sort Method

The sort method sorts the elements of an array according to the callback function.

For example:

```
function ascendingOrder(arr) {
  return arr.sort(function(a, b){
    return a - b;
  });
}
ascendingOrder([1, 5, 2, 3, 4]);
// Returns [1, 2, 3, 4, 5]

function reverseAlpha(arr) {
  return arr.sort(function (a, b) {
    return a < b;
  });
}
reverseAlpha(['l', 'h', 'z', 'b', 's']);
// returns ['z', 's', 'l', 'h', 'b']
```

Note: It's encouraging to provide a callback function to specify how to sort the array items. JavaScript's default sorting method is by string Unicode point value, which may return unexpected results. 
_____________________________________________________________________________
Use the sort method in the alphabeticalOrder function to sort the elements of arr in alphabetical order.
```
function alphabeticalOrder(arr) {
  // Add your code below this line
  return arr.sort(function(a, b) {
    return a > b;
  
  // Add your code above this line
}
alphabeticalOrder(["a", "d", "c", "a", "z", "g"]);

```

<div id="18a"/>

### Return a Sorted Array Without Changing the Original Array

A side effect of the sort method is that it changes the order of the elements in the original array. In other words, it mutates the array in place. One way to void this is to first concatenate an empty array to the one being sorted (remember that concat returns a new array), then run the sort method.
____________________________________________________________________
Use the sort method in the nonMutatingSort function to sort the elements of an array in ascending order. The function should return a new array, and not mutate the globalArray variable.

```
var globalArray = [5, 6, 3, 2, 9];
function nonMutatingSort(arr) {
  // Add your code below this line
  return arr.concat([]).sort(function(a, b) {
        return a > b;

  });
  
  // Add your code above this line
}
nonMutatingSort(globalArray);
```

<div id="19a"/>

### Split a String into an Array Using the split Method

The split method splits a string into an array of strings. It takes an argument for the delimiter, which can be a character to use to break up the string or a regular expression. For example, if the delimiter is a space, you get an array of words, and if the delimeter is an empty string, you get an array of each character in the string.

Here are two examples that split one string by spaces, then another by digits using a regular expression:

```
var str  = 'Hello World';
var bySpace = str.split(" ");
// sets bySpace to ["Hello", "World"]

var otherString = "How9are7you2today";
var byDigits = otherString.split(/\d/);
// Sets byDigits to ["How", "are", "you", "today"]
```
Since strings are immutable, the split method makes it easier to work with them.
_________________________________________________________________________________
Use the split method inside the splitify function to split str into an array of words. The function should return the array. Note that the words are not always separated by spaces, and the array should not contain punctuation.

```
function splitify(str) {
// Add your code below this line
      return str.split(/\W/);

// Add your code above this line
}
console.log(splitify("Hello World,I-am code"));
```

<div id="20a"/>

### Combine an Array into a String Using the join Method

The join method is used to join the elements of an array together to create a string. It takes an argument for the delimiter that is used to separate the array elements in the string.

Here's an example: 

```
var arr = ["Hello", "World"];
var str = arr.join(" ");
// Sets str to "Hello World"
```
______________________________________________________________________
Use the join method (among others) inside the sentensify function to make a sentence from the words in the string str. The function should return a string. For example, "I-like-Star-Wars" would be converted to "I like Star Wars". For this challenge, do not use the replace method.

```
function sentensify(str) {
  // Add your code below this line
  return str.split(/\W/).join(" ");
  
  // Add your code above this line
}
sentensify("May-the-force-be-with-you");
```

<div id="21a"/>

### Apply Functional Programming to Convert Strings to URL Slugs

The last several challenges covered a number of useful array methods that follow functional programming principles. We've also learned about reduce, which is a powerful method used to reduce problems to simpler forms. From computing averages to sorting, any array operation can be achieved by applying it. Recall that map and filter are special cases of reduce.

Let's combine what we've learned to solve a practical problem.

Many content management sites (CMS) have the titles of a post added to part of the URL for simple bookmarking purposes. For example, if you write a Medium post titles "Stop Using Reduce", it's likely the URL would have some form of the title string in it(".../stop-using-reduce"). You may have already noticed this on the freeCodeCamp site.
_______________________________________________________________________________
Fill in the urlSlug function so it converts a string title and returns the hyphenated version for the URL. You can use any of the methods covered in this section, and don't use replace. Here are the requirements:

The input is a string with spaces and title-cased words

The output is a string with the spaces between words replaced by a hyphen (-)

The output should be all lower-cased letters

The output should not have any spaces

```
// the global variable
var globalTitle = " Winter Is Coming";

// Add your code below this line
function urlSlug(title) {
// console.log(title.split(/\W/));   returns [ '', 'Winter', 'Is', 'Coming' ]
  return title.split(/\W/).filter(function(e) { // \W matches any non word
      return e !== '';        // filter loops through each element and return either true or false in this case it returns anything thats not falsey
// console.log(e !== '');  returns false true true true
  }).join('-').toLowerCase(); // then we join all words with - and convert to lower case
  
}
// Add your code above this line

var winterComing = urlSlug(globalTitle); // Should be "winter-is-coming"

console.log(winterComing);
console.log(urlSlug("A Mind Needs Books Like A Sword Needs A Whetstone"));
console.log(urlSlug("Hold The Door"));

```

<div id="22a"/>

### Use the every Method to Check that Every Element in an Array Meets a Criteria

The every method works with arrays to check if _every_ element passes a particular test. It returns a Boolean value -true if all values meet the criteria, false if not. 

For example, the following code would check if every element in the number array is less than 10:

```
var numbers = [1, 5, 8, 0, 10, 11];
numbers.every(function(currentValue) {
  return currentValue < 10;
});
// returns false
```
_________________________________________________________________
use the every method inside the checkPositive function to check if every element in arr is positive. The function should return a Boolean value.

```
function checkPositive(arr) {
  // Add your code below this line
  return arr.every(x => x > 0);
  
  // Add your code above this line
}
checkPositive([1, 2, 3, -4, 5]);
```

<div id="23a"/>

### Use the some Method to Check that Any Elements in an Array Meet a Criteria

The some method works with arrays to check if any element passes a particular test. It returns a Boolean value -true if any of the values meet the criteria, false if not.

For example, the following code would check if any element in the numbers array is less than 10:

```
var numbers = [10, 50, 8, 220, 110, 11];
numbers.some(function(currentValue) {
  return currentValue < 10;
});
// Returns true
```
____________________________________________________________________________________________________¨
Use the some method inside the checkPositive function to check if any element in arr is positive. The function should return a Boolean value.

```
function checkPositive(arr) {
  // Add your code below this line
  return arr.some(x => x > 0);
  
  // Add your code above this line
}
checkPositive([1, 2, 3, -4, 5]);

```

<div id="24a"/>

### Introduction to Currying and Partial Application 

The arity of a function is the number or arguments it requires. Currying a function means to convert a function of N arity into N functions of arity 1.

In other words, it restructures a function so it takes one argument, then returns another function that takes the next argument, and so on.

Here's an example:

```
// Un-curried function
function unCurried(x, y) {
  return x + y;
}

// Curried function
function curried(x) {
  return function(y) {
    return x + y;
  }
}

curried(1)(2) // Returns 3
```

This is useful in your program if you cant supply all the arguments to a function at one time. You can save each function call into a variable, which will hold the returned function reference that takes the next argument when it's available. Here's an example using the curried function in the example above:

```
// Call a curried function in parts:
var funcForY = curried(1);
console.log(funcForY(2)); // Prints 3
```

Similarly, partial application can be described as applying a few arguments to a function at a time and returning another function that is applied to more arguments.

Here's an example:

```
// Impartial function
function impartial(x, y, z) {
  return x + y + z;
}

var partialFn = impartial.bind(this, 1, 2);
partialFn(10); // Returns 13
```
___________________________________________________________
Fill in the body of the add function so it uses currying to add parameters x, y, and z.

```
function add(x) {
  // Add your code below this line
  return function(y) {
    return function(z) {
      return x + y + z;
    }
  }
  
  // Add your code above this line
}
add(10)(20)(30);
```

<div id="25a"/>

## Appendix Notes

**recursion** is when a function calls itself repeatedly to get a job done.

**closures** are where a function pulls values and references into from the outside (you know how there's a global i, then you run your function and it has access? that's where.)

**this** is the target of context.

so, like.

say you make a dog class.

class dog {};

say the dog class stores a name. if you have three instances of dog, each one gets its own name.

when you make a new dog, there has to be a way to refer to the stuff that's about this instance, rather than the other two. that's this.

class dog { constructor(name) { this._name = name; } };

the reason this gets so much flak in javascript is a few weird details weren't done in the convenient way in old-js, and they're some of the more common minefields for new programmers

but honestly it's pretty straightforward

---

<div id="sass"/>

# SASS

Table Of Contents:

1. [Introduction to the Sass Challenges](#1b)
2. [Sass: Store Data with Sass variables](#2b)
3. [Sass: Nesting CSS with Sass](#3b)
4. [Sass: Create Reusable CSS with Mixins](#4b)
5. [Sass: Use @if and @else to Add Logic To Your Styles](#5b)
6. [Sass: Use @for to Create a Sass Loop](#6b)
7. [Sass: Use @each to Map Over Items in a List](#7b)
8. [Apply a Style Until a Condition is Met with @while](#8b)
9. [Sass: Split Your Styles into Smaller Chunks with Partials](#9b)
10. [Sass: Extend One Set of CSS Styles to Another Element](#10b)

<div id="1b"/>

## Introduction to the Sass Challenges

Sass, or "Syntactically Awesome StyleSheets", is a language extension of CSS. It adds features that aren't available using basic CSS syntax. Sass makes it easier for developers to simplify and maintain the style sheets for their projects.

Sass can extend the CSS language because it is a preprocessor. It takes code written using Sass syntax, and converts it into basic CSS. This allows you to create variables, nest CSS rules into others, and import other Sass files, among other things. The result is more compact, easier to read code.

There are two syntaxes available for Sass. The first, known as SCSS (Sassy CSS) and used throughout these challenges, is an extension of the syntax of CSS. This means that every valid CSS stylesheet is a valid SCSS file with the same meaning. Files using this syntax have the .scss extension.

The second and older syntax, known as the indented syntax (or sometimes just "Sass"), uses indentation rather than brackets to indicate nesting of selectors, and newlines rather than semicolons to separate properties. Files using this syntax have the .sass extension.

This section introduces the basic features of Sass.


<div id="2b"/>

## Sass: Store Data with Sass variables

$main-fonts: Arial, sans-serif;
$heading-color: green;

```
// To use variables:
h1 {
    font-family: $main-fonts;
    color: $headings-color;
}

```

<div id="3b"/>

## Sass: Nesting CSS with Sass

```
nav {
    background-color: red;

    ul {
        list-style: none;

        li {
            display: inline-block;
        }
    }
}

```

<div id="4b"/>

## Sass: Create Reusable CSS with Mixins

```
@mixin box-shadow($x, $y, $blur, $c) {
    -webkit-box-shadow: $x, $y, $blur, $c;
    -moz-box-shadow: $x, $y, $blur, $c;
    -ms-box-shadow: $x, $y, $blur, $c;
    box-shadow: $x, $y, $blur, $c;
}

// A mixin is called with the @include directive:
div {
    @include box-shadow(0px, 0px, 4px, #fff);
}

```

<div id="5b"/>

## Sass: Use @if and @else to Add Logic To Your Styles

```
@mixin make-bold($bool) {
    @if $bool == true {
        font-weight: bold;
    }
}

// Like in JavaScript, @else if and @else test for more conditions

@mixin text-effect ($val) {
    @if $val == danger {
        color: red;
    }
    @else if $val == alert {
        color: yellow;
    }
    @else {
        color: black;
    }
}

```

<div id="6b"/>

## Sass: Use @for to Create a Sass Loop

@for is used in two ways: "start through end" or "start to end". The main difference is that
"start to end" excludes the end number, and "start through end" includes the end number.

Here's a start through end example:

```
@for $i for 1 through 12 {
    .col-#{$i} { width: 100%/12 * $i; }
}

```
The #{$i} part is the syntax to combine a variable (i) with the text to make a string. When the Sass file is converted to CSS. it looks like this: 

```
.col-1 {
    width: 8.33333%;
}

.col-2 {
    width: 16.66667%;
}

...

.col-12 {
    width: 100%
}
```
This is a powerful way to create a grid layout. Now you have twelve options for column widths available as CSS classes.

<div id="7b"/>

## Sass: Use @each to Map Over Items in a List

The last challenge showed how the @for directive uses a starting and ending value to loop a certain number of times. Sass also offers the @each directive which loops over each item in a list or map

On each iteration, the variable gets assigned to the current value from the list or map.

```
@each $color in blue, red, green {
    .#{$color}-text {color: $color;}
}

```
A map has slightly different syntax. Here's an example:

```
$colors: (color1: blue, color2: red, color3: green);

@each $key, $color in $colors {
    .#{$color}-text {color: $color;}
}
```

Note that the $key variable is needed to reference the keys in the map. Otherwise, the compiled CSS would have color1, color2... in it.

Both of the above code examples are converted into the following CSS:

```
.blue-text {
  color: blue;
}

.red-text {
  color: red;
}

.green-text {
  color: green;
}
```

<div id="8b"/>

## Apply a Style Until a Condition is Met with @while

The @while directive is an option with similar functionality to the JavaScript while loop. It creates CSS rules until a condition is met.

The @for challenge gave an example to create a simple grid system. This can also work with @while.

```
$x: 1;
@while $x < 13 {
    .col-#{$x} { width: 100%/12 * $x; }
    $x: $x +1;
}

```
First, define a variable $x and set it to 1. Next, use the @while directive to create the grid system while $x is less than 13.

After setting the CSS rule for width, $x is incremented by 1 to avoid an infinite loop.

<div id="9b"/>

## Sass: Split Your Styles into Smaller Chunks with Partials

Partials in Sass are separate files that hold segments of CSS code. These are imported and used in other Sass files. This is a great way to group similar code into a module to keep it organized.

Names for partials start with the underscore (_) character, which tells Sass it is a small segment of CSS and not to convert it into a CSS file. Also, Sass files end with the .scss file extension. To bring the code in the partial into another Sass file, use the @import directive.

For example, if all your mixins are saved in a partial named "_mixins.scss", and they are needed in the "main.scss" file, this is how to use them in the main file:

```
// In the main.scss file

@import 'mixins'
```

Note that the underscore is not needed in the import statement - Sass understands it is a partial. Once a partial is imported into a file, all variables, mixins, and other code are available to use.


<div id="10b"/>

## Sass: Extend One Set of CSS Styles to Another Element

Sass has a feature called extend that makes it easy to borrow the CSS rules from one element and build upon them in another.

For example, the below block of CSS rules style a .panel class. It has a background-color, height and border.

```
.panel {
    background-color: red;
    height: 70px;
    border: 2px solid green;
}
```

Now you want another panel called .big-panel. It has the same base properties as .panel, but also needs a width and font-size.

It's possible to copy and paste the initial CSS rules from .panel, but the code becomes repetitive as you add more types of panels.

The extend directive is a simple way to reuse the rules written for one element, then add more for another:

```
.big-panel {
    @extends .panel;
    width: 150px;
    font-size: 2em;
}
```

The .big-panel will have the same properties as .panel in addition to the new styles.


<div id="react"/>

# React

Table Of Contents:
1. [Introduction to the React Challenges](#1b)
2. [Create a Simple JSX Element](#2b)
3. [Create a Complex JSX Element](#3b)
4. [Add Comments in JSX](#4b)
5. [Render HTML Elements to the DOM](#5b)
6. [Define an HTML Class in JSX](#6b)
7. [Learn About Self-Closing JSX Tags](#7b)
8. [Create a Stateless Functional Component](#8b)
9. [Create a React Component](#9b)
10. [Create a Component with Composition](#10b)
11. [Use React to Render Nested Components](#11b)
12. [Compose React Components](#12b)
13. [Render a Class Component to the DOM](#13b)
14. [Write a React Component from Scratch](#14b)
15. [Pass Props to a Stateless Functional Component](#15b)
16. [Pass an Array as Props](#16b)
17. [Use Default Props](#17b)
18. [Override Default Props](#18b)
19. [Use PropTypes to Define the Props You Expect](#19b)
20. [Access Props Using this.props](#20b)
21. [Review Using Props with Stateless Functional Components](#21b)
22. [Create a Stateful Component](#22b)
23. [Render State in the User Interface](#23b)
24. [Render State in the User Interface Another Way](#24b)
25. [Set State with this.setState](#25b)
26. [Bind 'this' to a Class Method](#26b)
27. [Use State to Toggle an Element](#27b)
28. [Write a Simple Counter](#28b)
29. [Create a Controlled Input](#29b)
30. [Create a Controlled Form](#30b)
31. [Pass State as Props to Child Components](#31b)
32. [Pass a Callback as Props](#32)
33. [Use the Lifecycle Method componentWillMount](#33b)
34. [Use the Lifecycle Method componentDidMount](#34b)
35. [Add Event Listeners](#35b)
36. [Manage Updates with Lifecycle Methods](#36b)
37. [Optimize Re-Renders with shouldComponentUpdate](#37b)
38. [Introducing Inline Styles](#38b)
39. [Add Inline Styles in React](#39b)
40. [Use Advanced JavaScript in React Render Method](#40b)
41. [Render with an If/Else Condition](#41b)
42. [Use && for a More Concise Conditional](#42b)
43. [Use a Ternary Expression for Conditional Rendering](#43b)
44. [Render Conditionally from Props](#44b)
45. [Change Inline CSS Conditionally Based on Component State](#45b)
46. [Use Array.map() to Dynamically Render Elements](#46b)
47. [Give Sibling Elements a Unique Key Attribute](#47b)
48. [Use Array.filter() to Dynamically Filter an Array](#48b)
49. [Render React on the Server with renderToString](#49b)



<div id="1b"/>

## Introduction to the React Challenges

React, popularized by Facebook, is an open-source JavaScript library for building user interfaces. It is used to create components, handle state and props, utilize event listeners and certain life cycle methods to update data as it changes.

React combines HTML with JavaScript functionality to create its own markup language, JSX. This section will introduce you to all of these concepts and how to implement them for use with your own projects.


<div id="2b"/>

## Create a Simple JSX Element

Intro: React is an Open Source view library created and maintained by Facebook. It's a great tool to render the User Interface (UI) of modern web applications.

React uses a syntax extension of JavaScript called JSX that allows you to write HTML directly within JavaScript. This has several benefits. It lets you use the full programmatic power of JavaScript within HTML, and helps to keep your code readable. For the most part, JSX is similar to the HTML that you have already learned, however there are a few key differences that will be covered throughout these challenges.

For instance, because JSX is a syntactic extension of JavaScript, you can actually write JavaScript directly within JSX. To do this, you simply include the code you want to be treated as JavaScript within curly braces: { 'this is treated as JavaScript code' }

However, because JSX is not valid JavaScript, JSX code must be compiled into JavaScript. The transpiler Babel is a popular tool for this process.

It's worth noting that under the hood the challenges are calling ReactDOM.render(JSX, document.getElementById('root')). This function call is what places your JSX into React's own lightweight representation of the DOM. React then uses snapshots of its own DOM to optimize updating only specific parts of the actual DOM.

Instructions: The current code uses JSX to assign a div element to the constant JSX. Replace the div with an h1 element and add the text Hello JSX! inside it.

```
const JSX = <div></div>;

const JSX = <h1>Hello JSX!</h1>;
```

<div id="3b"/>

## Create a Complex JSX Element

The last challenge was a simple example of JSX, but JSX can represent more complex HTML as well.

One important thing to know about nested JSX is that it must return a single element.

This one parent element would wrap all of the other levels of nested elements.

For instance, several JSX elements written as siblings with no parent wrapper element will not transpile.

Here's an example:

Valid JSX:
```
<div>
    <p>Paragraph One</p>
    <p>Paragraph Two</p>
    <p>Paragraph Three</p>
</div>
```
Invalid JSX:
```
<p>Paragraph One</p>
<p>Paragraph Two</p>
<p>Paragraph Three</p>
```
Define a new constant JSX that renders a div which contains the following elements in order:

An h1, a p, and an unordered list that contains three li items. You can include any text you want within each element.

Note: When rendering multiple elements like this, you can wrap them all in parentheses, but it's not strictly required. Also notice this challenge uses a div tag to wrap all the child elements within a single parent element. If you remove the div, the JSX will no longer transpile. Keep this in mind, since it will also apply when you return JSX elements in React components.

```
const JSX = <div>
                <h1>Header</h1>
                <p>Paragraph</p>
                <ul>
                        <li>one</li>
                        <li>two</li>
                        <li>three</li>
                </ul>
            </div>;
```


<div id="4b"/>

## Add Comments in JSX

JSX is a syntax that gets compiled into valid JavaScript. Sometimes, for readability, you might need to add comments to your code. Like most programming languages, JSX has its own way to do this.

To put comments inside JSX, you use the syntax {/* */} to wrap around the comment text.

```
const JSX = (
  <div>
    <h1>This is a block of JSX</h1>
    {/*This is a comment*/}
    <p>Here's a subtitle</p>
  </div>
);
```

<div id="5b"/>

## Render HTML Elements to the DOM

So far, you've learned that JSX is a convenient tool to write readable HTML within JavaScript. With React, we can render this JSX directly to the HTML DOM using React's rendering API known as ReactDOM.

ReactDOM offers a simple method to render React elements to the DOM which looks like this: ReactDOM.render(componentToRender, targetNode), where the first argument is the React element or component that you want to render, and the second argument is the DOM node that you want to render the component to.

As you would expect, ReactDOM.render() must be called after the JSX element declarations, just like how you must declare variables before using them.

The code editor has a simple JSX component. Use the ReactDOM.render() method to render this component to the page. You can pass defined JSX elements directly in as the first argument and use document.getElementById() to select the DOM node to render them to. There is a div with id='challenge-node' available for you to use. Make sure you don't change the JSX constant.

```
const JSX = (
  <div>
    <h1>Hello World</h1>
    <p>Lets render this to the DOM</p>
  </div>
);
// change code below this line
// componentToRender => JSX
// targetNode => document.getElementById('challenge-node')
ReactDOM.render(JSX, document.getElementById('challenge-node'));
```


<div id="6b"/>

## Define an HTML Class in JSX

Now that you're getting comfortable writing JSX, you may be wondering how it differs from HTML.

So far, it may seem that HTML and JSX are exactly the same.

One key difference in JSX is that you can no longer use the word class to define HTML classes. This is because class is a reserved word in JavaScript. Instead, JSX uses className.

In fact, the naming convention for all HTML attributes and event references in JSX become camelCase. For example, a click event in JSX is onClick, instead of onclick. Likewise, onchange becomes onChange. While this is a subtle difference, it is an important one to keep in mind moving forward.

Apply a class of myDiv to the div provided in the JSX code.
```
const JSX = (
  <div className="myDiv">
    <h1>Add a class to this div</h1>
  </div>
);
```

<div id="7b"/>

## Learn About Self-Closing JSX Tags

So far, you’ve seen how JSX differs from HTML in a key way with the use of className vs. class for defining HTML classes.

Another important way in which JSX differs from HTML is in the idea of the self-closing tag.

In HTML, almost all tags have both an opening and closing tag: <div></div>; the closing tag always has a forward slash before the tag name that you are closing. However, there are special instances in HTML called “self-closing tags”, or tags that don’t require both an opening and closing tag before another tag can start.

For example the line-break tag can be written as <br> or as <br />, but should never be written as <br></br>, since it doesn't contain any content.

In JSX, the rules are a little different. Any JSX element can be written with a self-closing tag, and every element must be closed. The line-break tag, for example, must always be written as <br /> in order to be valid JSX that can be transpiled. A <div>, on the other hand, can be written as <div /> or <div></div>. The difference is that in the first syntax version there is no way to include anything in the <div />. You will see in later challenges that this syntax is useful when rendering React components.


<div id="8b"/>

## Create a Stateless Functional Component

Components are the core of React. Everything in React is a component and here you will learn how to create one.

There are two ways to create a React component. The first way is to use a JavaScript function. Defining a component in this way creates a stateless functional component. The concept of state in an application will be covered in later challenges. For now, think of a stateless component as one that can receive data and render it, but does not manage or track changes to that data. (We'll cover the second way to create a React component in the next challenge.)

To create a component with a function, you simply write a JavaScript function that returns either JSX or null. One important thing to note is that React requires your function name to begin with a capital letter. Here's an example of a stateless functional component that assigns an HTML class in JSX:

```
// After being transpiled, the <div> will have a CSS class of 'customClass'
const DemoComponent = function() {
  return (
    <div className='customClass' />
  );
};
```

Because a JSX component represents HTML, you could put several components together to create a more complex HTML page. This is one of the key advantages of the component architecture React provides. It allows you to compose your UI from many separate, isolated components. This makes it easier to build and maintain complex user interfaces.

The code editor has a function called MyComponent. Complete this function so it returns a single div element which contains some string of text.

Note: The text is considered a child of the div element, so you will not be able to use a self-closing tag.

```
const MyComponent = function() {
  // change code below this line
  return (
    <div>
      <p>This is some text.</p>
    </div>
  );


  // change code above this line
}
```

<div id="9b"/>

## Create a React Component

The other way to define a React component is with the ES6 class syntax. In the following example, Kitten extends React.Component:

```
class Kitten extends React.Component {
    constructor(props) {
        super(props);
    }

    render() {
        return (
            <h1>Hi</h1>
        );
    }
}
```
This creates an ES6 class Kitten which extends the React.Component class. So the Kitten class now has access to many useful React features, such as local state and lifecycle hooks. Don't worry if you aren't familiar with these terms yet, they will be covered in greater detail in later challenges.

Also notice the Kitten class has a constructor defined within it that calls super(). It uses super() to call the constructor of the parent class, in this case React.Component. The constructor is a special method used during the initialization of objects that are created with the class keyword. It is best practice to call a component's constructor with super, and pass props to both. This makes sure the component is initialized properly. For now, know that it is standard for this code to be included. Soon you will see other uses for the constructor as well as props.

MyComponent is defined in the code editor using class syntax. Finish writing the render method so it returns a div element that contains an h1 with the text Hello React!.
```
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    // change code below this line
      return (
        <div>
          <h1>Hello React!</h1>
        </div>
      );


    // change code above this line
  }
};
```


<div id="10b"/>

## Create a Component with Composition

Now we will look at how we can compose multiple React components together. Imagine you are building an App and have created three components, a Navbar, Dashboard, and Footer.

To compose these components together, you could create an App parent component which renders each of these three components as children. To render a component as a child in a React component, you include the component name written as a custom HTML tag in the JSX. For example, in the render method you could write:
```
return (
<App>
    <Navbar />
    <Dashboard />
    <Footer />
</App>
)
```
When React encounters a custom HTML tag that references another component (a component name wrapped in < /> like in this example), it renders the markup for that component in the location of the tag. This should illustrate the parent/child relationship between the App component and the Navbar, Dashboard, and Footer.

In the code editor, there is a simple functional component called ChildComponent and a React component called ParentComponent. Compose the two together by rendering the ChildComponent within the ParentComponent. Make sure to close the ChildComponent tag with a forward slash.

Note: ChildComponent is defined with an ES6 arrow function because this is a very common practice when using React. However, know that this is just a function. If you aren't familiar with the arrow function syntax, please refer to the JavaScript section.
```
const ChildComponent = () => {
  return (
    <div>
      <p>I am the child</p>
    </div>
  );
};

class ParentComponent extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h1>I am the parent</h1>
        { /* change code below this line */ }
        <ChildComponent />

        { /* change code above this line */ }
      </div>
    );
  }
};
```

<div id="11b"/>

## Use React to Render Nested Components

The last challenge showed a simple way to compose two components, but there are many different ways you can compose components with React.

Component composition is one of React's powerful features. When you work with React, it is important to start thinking about your user interface in terms of components like the App example in the last challenge. You break down your UI into its basic building blocks, and those pieces become the components. This helps to separate the code responsible for the UI from the code responsible for handling your application logic. It can greatly simplify the development and maintenance of complex projects.

There are two functional components defined in the code editor, called TypesOfFruit and Fruits. Take the TypesOfFruit component and compose it, or nest it, within the Fruits component. Then take the Fruits component and nest it within the TypesOfFood component. The result should be a child component, nested within a parent component, which is nested within a parent component of its own!
```
const TypesOfFruit = () => {
  return (
    <div>
      <h2>Fruits:</h2>
      <ul>
        <li>Apples</li>
        <li>Blueberries</li>
        <li>Strawberries</li>
        <li>Bananas</li>
      </ul>
    </div>
  );
};

const Fruits = () => {
  return (
    <div>
      { /* change code below this line */ }
      <TypesOfFruit />
      { /* change code above this line */ }
    </div>
  );
};

class TypesOfFood extends React.Component {
  constructor(props) {
    super(props);
  }

  render() {
    return (
      <div>
        <h1>Types of Food:</h1>
        { /* change code below this line */ }
        <Fruits />
        { /* change code above this line */ }
      </div>
    );
  }
};
```


<div id="12b"/>

## Compose React Components

As the challenges continue to use more complex compositions with React components and JSX, there is one important point to note. Rendering ES6 style class components within other components is no different than rendering the simple components you used in the last few challenges. You can render JSX elements, stateless functional components, and ES6 class components within other components.

In the code editor, the TypesOfFood component is already rendering a component called Vegetables. Also, there is the Fruits component from the last challenge.

Nest two components inside of Fruits — first NonCitrus, and then Citrus. Both of these components are provided for you in the background. Next, nest the Fruits class component into the TypesOfFood component, below the h1 header and above Vegetables. The result should be a series of nested components, which uses two different component types.
```
class Fruits extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h2>Fruits:</h2>
        { /* change code below this line */ }
        <NonCitrus />
        <Citrus />
         { /* change code above this line */ }
      </div>
    );
  }
};

class TypesOfFood extends React.Component {
  constructor(props) {
     super(props);
  }
  render() {
    return (
      <div>
        <h1>Types of Food:</h1>
        { /* change code below this line */ }
        <Fruits />
        { /* change code above this line */ }
        <Vegetables />
      </div>
    );
  }
};
```


<div id="13b"/>

## Render a Class Component to the DOM

You may remember using the ReactDOM API in an earlier challenge to render JSX elements to the DOM. The process for rendering React components will look very similar. The past few challenges focused on components and composition, so the rendering was done for you behind the scenes. However, none of the React code you write will render to the DOM without making a call to the ReactDOM API.

Here's a refresher on the syntax: ReactDOM.render(componentToRender, targetNode). The first argument is the React component that you want to render. The second argument is the DOM node that you want to render that component within.

React components are passed into ReactDOM.render() a little differently than JSX elements. For JSX elements, you pass in the name of the element that you want to render. However, for React components, you need to use the same syntax as if you were rendering a nested component, for example ReactDOM.render(<ComponentToRender />, targetNode). You use this syntax for both ES6 class components and functional components.

Both the Fruits and Vegetables components are defined for you behind the scenes. Render both components as children of the TypesOfFood component, then render TypesOfFood to the DOM. There is a div with id='challenge-node' available for you to use.

```
class TypesOfFood extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h1>Types of Food:</h1>
        {/* change code below this line */}
        <Fruits />
        <Vegetables />
        {/* change code above this line */}
      </div>
    );
  }
};

// change code below this line
ReactDOM.render(<TypesOfFood />, document.getElementById('challenge-node'))

```

<div id="14b"/>

## Write a React Component from Scratch

Now that you've learned the basics of JSX and React components, it's time to write a component on your own. React components are the core building blocks of React applications so it's important to become very familiar with writing them. Remember, a typical React component is an ES6 class which extends React.Component. It has a render method that returns HTML (from JSX) or null. This is the basic form of a React component. Once you understand this well, you will be prepared to start building more complex React projects.

Define a class MyComponent that extends React.Component. Its render method should return a div that contains an h1 tag with the text: My First React Component! in it. Use this text exactly, the case and punctuation matter. Make sure to call the constructor for your component, too.

Render this component to the DOM using ReactDOM.render(). There is a div with id='challenge-node' available for you to use.
```
// change code below this line
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h1>My First React Component!</h1>
      </div>
    );
  }
};

ReactDOM.render(<MyComponent />, document.getElementById('challenge-node'));
```

<div id="15b"/>

## Pass Props to a Stateless Functional Component

The previous challenges covered a lot about creating and composing JSX elements, functional components, and ES6 style class components in React. With this foundation, it's time to look at another feature very common in React: props. In React, you can pass props, or properties, to child components. Say you have an App component which renders a child component called Welcome that is a stateless functional component. You can pass Welcome a user property by writing:

```
<App>
    <Welcome user='Mark' />
</App>
```
You use custom HTML attributes that React provides support for to pass the property user to the component Welcome. Since Welcome is a stateless functional component, it has access to this value like so:
```
const Welcome = (props) => <h1>Hello, {props.user}</h1>
```
It is standard to call this value props and when dealing with stateless functional components, you basically consider it as an argument to a function which returns JSX. You can access the value of the argument in the function body. With class components, you will see this is a little different.

There are Calendar and CurrentDate components in the code editor. When rendering CurrentDate from the Calendar component, pass in a property of date assigned to the current date from JavaScript's Date object. Then access this prop in the CurrentDate component, showing its value within the p tags. Note that for prop values to be evaluated as JavaScript, they must be enclosed in curly brackets, for instance date={Date()}.
```

const CurrentDate = (props) => {
  return (
    <div>
      { /* change code below this line */ }
      <p>The current date is: {props.date} </p>
      { /* change code above this line */ }
    </div>
  );
};

class Calendar extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h3>What date is it?</h3>
        { /* change code below this line */ }
        <CurrentDate date={Date()}/>
        { /* change code above this line */ }
      </div>
    );
  }
};
```


<div id="16b"/>

## Pass an Array as Props

The last challenge demonstrated how to pass information from a parent component to a child component as props or properties. This challenge looks at how arrays can be passed as props. To pass an array to a JSX element, it must be treated as JavaScript and wrapped in curly braces.
```
<ParentComponent>
  <ChildComponent colors={["green", "blue", "red"]} />
</ParentComponent>
```
The child component then has access to the array property colors. Array methods such as join() can be used when accessing the property.
```
const ChildComponent = (props) => <p>{props.colors.join(', ')}</p>
```
This will join all colors array items into a comma separated string and produce:
```
<p>green, blue, red</p>
```
Later, we will learn about other common methods to render arrays of data in React.

There are List and ToDo components in the code editor. When rendering each List from the ToDo component, pass in a tasks property assigned to an array of to-do tasks, for example ["walk dog", "workout"]. Then access this tasks array in the List component, showing its value within the p element. Use join(", ") to display the props.tasksarray in the p element as a comma separated list. Today's list should have at least 2 tasks and tomorrow's should have at least 3 tasks.
```
const List= (props) => {
  { /* change code below this line */ }
  return <p>{props.tasks.join(", ")}</p>
  { /* change code above this line */ }
};

class ToDo extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h1>To Do Lists</h1>
        <h2>Today</h2>
        { /* change code below this line */ }
        <List tasks={["walk dog", "workout"]}/>
        <h2>Tomorrow</h2>
        <List tasks={["workout", "work on project", "walk dog"]}/>
        { /* change code above this line */ }
      </div>
    );
  }
};
```

<div id="17b"/>

## Use Default Props

React also has an option to set default props. You can assign default props to a component as a property on the component itself and React assigns the default prop if necessary. This allows you to specify what a prop value should be if no value is explicitly provided. For example, if you declare MyComponent.defaultProps = { location: 'San Francisco' }, you have defined a location prop that's set to the string San Francisco, unless you specify otherwise. React assigns default props if props are undefined, but if you pass null as the value for a prop, it will remain null.

The code editor shows a ShoppingCart component. Define default props on this component which specify a prop items with a value of 0.
```
const ShoppingCart = (props) => {
  return (
    <div>
      <h1>Shopping Cart Component</h1>
    </div>
  )
};
// change code below this line
ShoppingCart.defaultProps = { items: 0 }
```


<div id="18b"/>

## Override Default Props

The ability to set default props is a useful feature in React. The way to override the default props is to explicitly set the prop values for a component.

The ShoppingCart component now renders a child component Items. This Items component has a default prop quantity set to the integer 0. Override the default prop by passing in a value of 10 for quantity.

Note: Remember that the syntax to add a prop to a component looks similar to how you add HTML attributes. However, since the value for quantity is an integer, it won't go in quotes but it should be wrapped in curly braces. For example, {100}. This syntax tells JSX to interpret the value within the braces directly as JavaScript.
```
const Items = (props) => {
  return <h1>Current Quantity of Items in Cart: {props.quantity}</h1>
}

Items.defaultProps = {
  quantity: 0
}

class ShoppingCart extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    { /* change code below this line */ }
    return <Items quantity={ 10 }/>
    { /* change code above this line */ }
  }
};
```


<div id="19b"/>

## Use PropTypes to Define the Props You Expect

React provides useful type-checking features to verify that components receive props of the correct type. For example, your application makes an API call to retrieve data that you expect to be in an array, which is then passed to a component as a prop. You can set propTypes on your component to require the data to be of type array. This will throw a useful warning when the data is of any other type.

It's considered a best practice to set propTypes when you know the type of a prop ahead of time. You can define a propTypes property for a component in the same way you defined defaultProps. Doing this will check that props of a given key are present with a given type. Here's an example to require the type function for a prop called handleClick:
```
MyComponent.propTypes =  { handleClick: PropTypes.func.isRequired }
```
In the example above, the PropTypes.func part checks that handleClick is a function. Adding isRequired tells React that handleClick is a required property for that component. You will see a warning if that prop isn't provided. Also notice that func represents function. Among the seven JavaScript primitive types, function and boolean (written as bool) are the only two that use unusual spelling. In addition to the primitive types, there are other types available. For example, you can check that a prop is a React element. Please refer to the documentation for all of the options.

Note: As of React v15.5.0, PropTypes is imported independently from React, like this:
```
import React, { PropTypes } from 'react';
```
Define propTypes for the Items component to require quantity as a prop and verify that it is of type number.
```
const Items = (props) => {
  return <h1>Current Quantity of Items in Cart: {props.quantity}</h1>
};

// change code below this line
Items.propTypes = { quantity: PropTypes.number.isRequired }
// change code above this line

Items.defaultProps = {
  quantity: 0
};

class ShoppingCart extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return <Items />
  }
};
```

<div id="20b"/>

## Access Props Using this.props

The last several challenges covered the basic ways to pass props to child components. But what if the child component that you're passing a prop to is an ES6 class component, rather than a stateless functional component? The ES6 class component uses a slightly different convention to access props.

Anytime you refer to a class component within itself, you use the this keyword. To access props within a class component, you preface the code that you use to access it with this. For example, if an ES6 class component has a prop called data, you write {this.props.data} in JSX.

Render an instance of the ReturnTempPassword component in the parent component ResetPassword. Here, give ReturnTempPassword a prop of tempPassword and assign it a value of a string that is at least 8 characters long. Within the child, ReturnTempPassword, access the tempPassword prop within the strong tags to make sure the user sees the temporary password.
```
class ReturnTempPassword extends React.Component {
  constructor(props) {
    super(props);

  }
  render() {
    return (
        <div>
            { /* change code below this line */ }
            <p>Your temporary password is: 
              <strong>{this.props.tempPassword}</strong>
            </p>
            { /* change code above this line */ }
        </div>
    );
  }
};

class ResetPassword extends React.Component {
  constructor(props) {
    super(props);

  }
  render() {
    return (
        <div>
          <h2>Reset Password</h2>
          <h3>We've generated a new temporary password for you.</h3>
          <h3>Please reset this password from your account settings ASAP.</h3>
          { /* change code below this line */ }
          <ReturnTempPassword tempPassword={"asdfjklö"}/>
          { /* change code above this line */ }
        </div>
    );
  }
};
```

<div id="21b"/>

## Review Using Props with Stateless Functional Components

Except for the last challenge, you've been passing props to stateless functional components. These components act like pure functions. They accept props as input and return the same view every time they are passed the same props. You may be wondering what state is, and the next challenge will cover it in more detail. Before that, here's a review of the terminology for components.

A stateless functional component is any function you write which accepts props and returns JSX. A stateless component, on the other hand, is a class that extends React.Component, but does not use internal state (covered in the next challenge). Finally, a stateful component is any component that does maintain its own internal state. You may see stateful components referred to simply as components or React components.

A common pattern is to try to minimize statefulness and to create stateless functional components wherever possible. This helps contain your state management to a specific area of your application. In turn, this improves development and maintenance of your app by making it easier to follow how changes to state affect its behavior.

```
class CampSite extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <Camper />
      </div>
    );
  }
};
// change code below this line

const Camper = (props) => {
  return <p>{props.name}</p>
};

Camper.propTypes = { name: PropTypes.string.isRequired };

Camper.defaultProps = {
  name: 'CamperBot'
};

```

<div id="22b"/>

## Create a Stateful Component

One of the most important topics in React is state. State consists of any data your application needs to know about, that can change over time. You want your apps to respond to state changes and present an updated UI when necessary. React offers a nice solution for the state management of modern web applications.

You create state in a React component by declaring a state property on the component class in its constructor. This initializes the component with state when it is created. The state property must be set to a JavaScript object. Declaring it looks like this:
```
this.state = {
  // describe your state here
}
```
You have access to the state object throughout the life of your component. You can update it, render it in your UI, and pass it as props to child components. The state object can be as complex or as simple as you need it to be. Note that you must create a class component by extending React.Component in order to create state like this.

There is a component in the code editor that is trying to render a name property from its state. However, there is no state defined. Initialize the component with state in the constructor and assign your name to a property of name.
```
class StatefulComponent extends React.Component {
  constructor(props) {
    super(props);
    // initialize state here
    this.state = {
     name: 'Name'
    }

  }
  render() {
    return (
      <div>
        <h1>{this.state.name}</h1>
      </div>
    );
  }
};
```

<div id="23b"/>

## Render State in the User Interface

Once you define a component's initial state, you can display any part of it in the UI that is rendered. If a component is stateful, it will always have access to the data in state in its render() method. You can access the data with this.state.

If you want to access a state value within the return of the render method, you have to enclose the value in curly braces.

State is one of the most powerful features of components in React. It allows you to track important data in your app and render a UI in response to changes in this data. If your data changes, your UI will change. React uses what is called a virtual DOM, to keep track of changes behind the scenes. When state data updates, it triggers a re-render of the components using that data - including child components that received the data as a prop. React updates the actual DOM, but only where necessary. This means you don't have to worry about changing the DOM. You simply declare what the UI should look like.

Note that if you make a component stateful, no other components are aware of its state. Its state is completely encapsulated, or local to that component, unless you pass state data to a child component as props. This notion of encapsulated state is very important because it allows you to write certain logic, then have that logic contained and isolated in one place in your code.

In the code editor, MyComponent is already stateful. Define an h1 tag in the component's render method which renders the value of name from the component's state.

Note: The h1 should only render the value from state and nothing else. In JSX, any code you write with curly braces { } will be treated as JavaScript. So to access the value from state just enclose the reference in curly braces.
```
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      name: 'freeCodeCamp'
    }
  }
  render() {
    return (
      <div>
        { /* change code below this line */ }
        <h1>{this.state.name}</h1>
        { /* change code above this line */ }
      </div>
    );
  }
};
```

<div id="24b"/>

## Render State in the User Interface Another Way

There is another way to access state in a component. In the render() method, before the return statement, you can write JavaScript directly. For example, you could declare functions, access data from state or props, perform computations on this data, and so on. Then, you can assign any data to variables, which you have access to in the return statement.

In the MyComponent render method, define a const called name and set it equal to the name value in the component's state. Because you can write JavaScript directly in this part of the code, you don't have to enclose this reference in curly braces.

Next, in the return statement, render this value in an h1 tag using the variable name. Remember, you need to use the JSX syntax (curly braces for JavaScript) in the return statement.
```
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      name: 'freeCodeCamp'
    }
  }
  render() {
    // change code below this line
    const name = this.state.name;
    // change code above this line
    return (
      <div>
        { /* change code below this line */ }
          <h1>{name}</h1>
        { /* change code above this line */ }
      </div>
    );
  }
};
```

<div id="25b"/>

## Set State with this.setState

The previous challenges covered component state and how to initialize state in the constructor. There is also a way to change the component's state. React provides a method for updating component state called setState. You call the setState method within your component class like so: this.setState(), passing in an object with key-value pairs. The keys are your state properties and the values are the updated state data. For instance, if we were storing a username in state and wanted to update it, it would look like this:
```
this.setState({
  username: 'Lewis'
});
```
React expects you to never modify state directly, instead always use this.setState() when state changes occur. Also, you should note that React may batch multiple state updates in order to improve performance. What this means is that state updates through the setState method can be asynchronous. There is an alternative syntax for the setState method which provides a way around this problem. This is rarely needed but it's good to keep it in mind! Please consult the [React documentation](https://reactjs.org/docs/state-and-lifecycle.html) for further details.

There is a button element in the code editor which has an onClick() handler. This handler is triggered when the button receives a click event in the browser, and runs the handleClick method defined on MyComponent. Within the handleClick method, update the component state using this.setState(). Set the name property in state to equal the string React Rocks!.

Click the button and watch the rendered state update. Don't worry if you don't fully understand how the click handler code works at this point. It's covered in upcoming challenges.

```
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      name: 'Initial State'
    };
    this.handleClick = this.handleClick.bind(this);
  }
  handleClick() {
    // change code below this line
      this.setState({name: 'React Rocks!'});
    // change code above this line
  }
  render() {
    return (
      <div>
        <button onClick={this.handleClick}>Click Me</button>
        <h1>{this.state.name}</h1>
      </div>
    );
  }
};
```

<div id="26b"/>

## Bind 'this' to a Class Method

In addition to setting and updating state, you can also define methods for your component class. A class method typically needs to use the this keyword so it can access properties on the class (such as state and props) inside the scope of the method. There are a few ways to allow your class methods to access this.

One common way is to explicitly bind this in the constructor so this becomes bound to the class methods when the component is initialized. You may have noticed the last challenge used this.handleClick = this.handleClick.bind(this) for its handleClick method in the constructor. Then, when you call a function like this.setState() within your class method, this refers to the class and will not be undefined.

Note: The this keyword is one of the most confusing aspects of JavaScript but it plays an important role in React. Although its behavior here is totally normal, these lessons aren't the place for an in-depth review of this so please refer to other lessons if the above is confusing!

The code editor has a component with a state that keeps track of an item count. It also has a method which allows you to increment this item count. However, the method doesn't work because it's using the this keyword that is undefined. Fix it by explicitly binding this to the addItem() method in the component's constructor.

Next, add a click handler to the button element in the render method. It should trigger the addItem() method when the button receives a click event. Remember that the method you pass to the onClick handler needs curly braces because it should be interpreted directly as JavaScript.

Once you complete the above steps you should be able to click the button and see the item count increment in the HTML.
```
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      itemCount: 0
    };
    // change code below this line
    this.addItem = this.addItem.bind(this);
    // change code above this line
  }
  addItem() {
    this.setState({
      itemCount: this.state.itemCount + 1
    });
  }
  render() {
    return (
      <div>
        { /* change code below this line */ }
        <button onClick={this.addItem}>Click Me</button>
        { /* change code above this line */ }
        <h1>Current Item Count: {this.state.itemCount}</h1>
      </div>
    );
  }
};
```

<div id="27b"/>

## Use State to Toggle an Element

You can use state in React applications in more complex ways than what you've seen so far. One example is to monitor the status of a value, then render the UI conditionally based on this value. There are several different ways to accomplish this, and the code editor shows one method.

MyComponent has a visibility property which is initialized to false. The render method returns one view if the value of visibility is true, and a different view if it is false.

Currently, there is no way of updating the visibility property in the component's state. The value should toggle back and forth between true and false. There is a click handler on the button which triggers a class method called toggleVisibility(). Define this method so the state of visibility toggles to the opposite value when the method is called. If visibility is false, the method sets it to true, and vice versa.

Finally, click the button to see the conditional rendering of the component based on its state.

Hint: Don't forget to bind the this keyword to the method in the constructor!
```
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      visibility: false
    };
    // change code below this line
    this.toggleVisibility = this.toggleVisibility.bind(this);
    // change code above this line
  }
  // change code below this line
  toggleVisibility() {
    if (this.state.visibility == true) {
      this.setState({
        visibility: false
      });
    } else {
      this.setState({
        visibility: true
      });
    }
  }
  // change code above this line
  render() {
    if (this.state.visibility) {
      return (
        <div>
          <button onClick={this.toggleVisibility}>Click Me</button>
          <h1>Now you see me!</h1>
        </div>
      );
    } else {
      return (
        <div>
          <button onClick={this.toggleVisibility}>Click Me</button>
        </div>
      );
    }
  }
};
```

<div id="28b"/>

## Write a Simple Counter

You can design a more complex stateful component by combining the concepts covered so far. These include initializing state, writing methods that set state, and assigning click handlers to trigger these methods.

The Counter component keeps track of a count value in state. There are two buttons which call methods increment() and decrement(). Write these methods so the counter value is incremented or decremented by 1 when the appropriate button is clicked. Also, create a reset() method so when the reset button is clicked, the count is set to 0.

Note: Make sure you don't modify the classNames of the buttons. Also, remember to add the necessary bindings for the newly-created methods in the constructor.

```
class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
    // change code below this line
    this.increment = this.increment.bind(this);
    this.decrement = this.decrement.bind(this);
    this.reset = this.reset.bind(this)
    // change code above this line
  }
  // change code below this line
  increment(){this.setState({count: this.state.count +1});}
  decrement(){this.setState({count: this.state.count -1});}
  reset(){this.setState({count: 0});}
  // change code above this line
  render() {
    return (
      <div>
        <button className='inc' onClick={this.increment}>Increment!</button>
        <button className='dec' onClick={this.decrement}>Decrement!</button>
        <button className='reset' onClick={this.reset}>Reset</button>
        <h1>Current Count: {this.state.count}</h1>
      </div>
    );
  }
};
```

<div id="29b"/>

## Create a Controlled Input

Your application may have more complex interactions between state and the rendered UI. For example, form control elements for text input, such as input and textarea, maintain their own state in the DOM as the user types. With React, you can move this mutable state into a React component's state. The user's input becomes part of the application state, so React controls the value of that input field. Typically, if you have React components with input fields the user can type into, it will be a controlled input form.

The code editor has the skeleton of a component called ControlledInput to create a controlled input element. The component's state is already initialized with an input property that holds an empty string. This value represents the text a user types into the input field.

First, create a method called handleChange() that has a parameter called event. When the method is called, it receives an event object that contains a string of text from the input element. You can access this string with event.target.value inside the method. Update the input property of the component's state with this new string.

In the render method, create the input element above the h4 tag. Add a value attribute which is equal to the input property of the component's state. Then add an onChange() event handler set to the handleChange() method.

When you type in the input box, that text is processed by the handleChange() method, set as the input property in the local state, and rendered as the value in the input box on the page. The component state is the single source of truth regarding the input data.

Last but not least, don't forget to add the necessary bindings in the constructor.
```
class ControlledInput extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      input: ''
    };
    // change code below this line
    this.handleChange = this.handleChange.bind(this);
    // change code above this line
  }
  // change code below this line
  handleChange(event) {
    this.setState({
      input: event.target.value
    });
  }
  // change code above this line
  render() {
    return (
      <div>
        { /* change code below this line */}
        <input value={this.state.input} onChange={this.handleChange}></input>
        { /* change code above this line */}
        <h4>Controlled Input:</h4>
        <p>{this.state.input}</p>
      </div>
    );
  }
};
```

<div id="30b"/>

## Create a Controlled Form

The last challenge showed that React can control the internal state for certain elements like input and textarea, which makes them controlled components. This applies to other form elements as well, including the regular HTML form element.

The MyForm component is set up with an empty form with a submit handler. The submit handler will be called when the form is submitted.

We've added a button which submits the form. You can see it has the type set to submit indicating it is the button controlling the form. Add the input element in the form and set its value and onChange() attributes like the last challenge. You should then complete the handleSubmit method so that it sets the component state property submit to the current input value in the local state.

Note:  You also must call event.preventDefault() in the submit handler, to prevent the default form submit behavior which will refresh the web page.

Finally, create an h1 tag after the form which renders the submit value from the component's state. You can then type in the form and click the button (or press enter), and you should see your input rendered to the page.
```
class MyForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      input: '',
      submit: ''
    };
    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }
  handleChange(event) {
    this.setState({
      input: event.target.value
    });
  }
  handleSubmit(event) {
    // change code below this line
    event.preventDefault();
    this.setState({
      input: '',
      submit: this.state.input
    });
    // change code above this line
  }
  render() {
    return (
      <div>
        <form onSubmit={this.handleSubmit}>
          { /* change code below this line */ }
          <input 
            value={this.state.input} 
            onChange={this.handleChange}
            />
          { /* change code above this line */ }
          <button type='submit'>Submit!</button>
        </form>
        { /* change code below this line */ }
        <h1>{this.state.submit}</h1>
        { /* change code above this line */ }
      </div>
    );
  }
};
```
Creating a controlled form is the same process as creating a controlled input, except you need to handle a submit event.

First, create a controlled input that stores its value in state, so that there is a single source of truth. (This is what you did in the previous challenge.) Create an input element, set it’s value attribute to the input variable located in state. Remember, state can be accessed by this.state. Next, set the input element’s onChange attribute to call the function ‘handleChange’.
```
<input value={this.state.input} onChange={this.handleChange}/>
```
Next, create the handleSubmit method for your component. First, because your form is submitting you will have to prevent the page from refreshing. Second, call the setState() method, passing in an object of the different key-value pairs that you want to change. In this case, you want to set ‘submit’ to the value of the variable ‘input’ and set ‘input’ to an empty string. 
```
handleSubmit(event) {
  event.preventDefault();
  this.setState({
    input: '',
    submit: this.state.input
  });
}
```
Now that your data is being handled in state, we can use this data. Create an h1 element. Inside of your h1 element put your ‘submit’ variable. Remember, ‘submit’ is located within state so you’ll need to use this.state. Additionally, placing the variable within JSX requires curly braces { } because it is JavaScript. 
```
<h1>{this.state.submit}</h1>
```

<div id="31b"/>

## Pass State as Props to Child Components

You saw a lot of examples that passed props to child JSX elements and child React components in previous challenges. You may be wondering where those props come from. A common pattern is to have a stateful component containing the state important to your app, that then renders child components. You want these components to have access to some pieces of that state, which are passed in as props.

For example, maybe you have an App component that renders a Navbar, among other components. In your App, you have state that contains a lot of user information, but the Navbar only needs access to the user's username so it can display it. You pass that piece of state to the Navbar component as a prop.

This pattern illustrates some important paradigms in React. The first is unidirectional data flow. State flows in one direction down the tree of your application's components, from the stateful parent component to child components. The child components only receive the state data they need. The second is that complex stateful apps can be broken down into just a few, or maybe a single, stateful component. The rest of your components simply receive state from the parent as props, and render a UI from that state. It begins to create a separation where state management is handled in one part of code and UI rendering in another. This principle of separating state logic from UI logic is one of React's key principles. When it's used correctly, it makes the design of complex, stateful applications much easier to manage.

The MyApp component is stateful and renders a Navbar component as a child. Pass the name property in its state down to the child component, then show the name in the h1 tag that's part of the Navbar render method.

In this challenge we are going to be passing state, but since state is local to its parent component we must use props to pass into the child component. Using props in child components will allow us to keep all the state data in the parent component and we can pass the data in one direction to the children components.
```
class MyApp extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      name: 'CamperBot'
    }
  }
  render() {
    return (
       <div>
         // Here we will call this.state.name in order to pass the value of CamperBot
         // to the NavBar component
         <Navbar name={this.state.name} />
       </div>
    );
  }
};

class Navbar extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
    <div>
      // Since we passed in the CamperBot state value into the the NavBar component above
      // the h1 element below will render the value passed from state
      <h1>Hello, my name is: {this.props.name}</h1>
    </div>
    );
  }
};

```


<div id="32b"/>

## Pass a Callback as Props

You can pass state as props to child components, but you're not limited to passing data. You can also pass handler functions or any method that's defined on a React component to a child component. This is how you allow child components to interact with their parent components. You pass methods to a child just like a regular prop. It's assigned a name and you have access to that method name under this.props in the child component.

There are three components outlined in the code editor. The MyApp component is the parent that will render the GetInput and RenderInput child components. Add the GetInput component to the render method in MyApp, then pass it a prop called input assigned to inputValue from MyApp's state. Also create a prop called handleChange and pass the input handler handleChange to it.

Next, add RenderInput to the render method in MyApp, then create a prop called input and pass the inputValue from state to it. Once you are finished you will be able to type in the input field in the GetInput component, which then calls the handler method in its parent via props. This updates the input in the state of the parent, which is passed as props to both children. Observe how the data flows between the components and how the single source of truth remains the state of the parent component. Admittedly, this example is a bit contrived, but should serve to illustrate how data and callbacks can be passed between React components.
```
class MyApp extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      inputValue: ''
    }
    this.handleChange = this.handleChange.bind(this);
  }
  handleChange(event) {
    this.setState({
      inputValue: event.target.value
    });
  }
  render() {
    return (
       <div>
        { /* change code below this line */ }
        <GetInput 
          input={this.state.inputValue} 
          handleChange={this.handleChange}
        />
        <RenderInput input={this.state.inputValue}/>
        { /* change code above this line */ }
       </div>
    );
  }
};

class GetInput extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h3>Get Input:</h3>
        <input
          value={this.props.input}
          onChange={this.props.handleChange}/>
      </div>
    );
  }
};

class RenderInput extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h3>Input Render:</h3>
        <p>{this.props.input}</p>
      </div>
    );
  }
};
```

**Description**

* Add the GetInput component to the render method in MyApp, then pass it a prop called input assigned to inputValue from MyApp’s state. Also create a prop called handleChange and pass the input handler handleChange to it.
* Add RenderInput to the render method in MyApp, then create a prop called input and pass the inputValue from state to it.

**Hints**

* state is a property of Myapp class, so use ‘this.state’ to get the object value
* To learn more about state and props, read [State and Lifecycle](https://reactjs.org/docs/state-and-lifecycle.html) and [Components and Props](https://reactjs.org/docs/components-and-props.html).

```
 render() {
    return (
       <div>
        { /* change code below this line */ 
        <GetInput input={this.state.inputValue} handleChange={this.handleChange}/>
        }
        { /* change code above this line */ 
        <RenderInput input={this.state.inputValue}/>
        }
       </div>
    );
  }
```

<div id="33b"/>

## Use the Lifecycle Method componentWillMount

React components have several special methods that provide opportunities to perform actions at specific points in the lifecycle of a component. These are called lifecycle methods, or lifecycle hooks, and allow you to catch components at certain points in time. This can be before they are rendered, before they update, before they receive props, before they unmount, and so on. Here is a list of some of the main lifecycle methods:

componentWillMount()

componentDidMount()

componentWillReceiveProps()

shouldComponentUpdate()

componentWillUpdate()

componentDidUpdate()

componentWillUnmount()

The next several lessons will cover some of the basic use cases for these lifecycle methods.

The componentWillMount() method is called before the render() method when a component is being mounted to the DOM. Log something to the console within componentWillMount() - you may want to have your browser console open to see the output.
```
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
  }
  componentWillMount() {
    // change code below this line
    console.log("Hello World")
    // change code above this line
  }
  render() {
    return <div />
  }
};
```

<div id="34b"/>

## Use the Lifecycle Method componentDidMount

Most web developers, at some point, need to call an API endpoint to retrieve data. If you're working with React, it's important to know where to perform this action.

The best practice with React is to place API calls or any calls to your server in the lifecycle method componentDidMount(). This method is called after a component is mounted to the DOM. Any calls to setState() here will trigger a re-rendering of your component. When you call an API in this method, and set your state with the data that the API returns, it will automatically trigger an update once you receive the data.

There is a mock API call in componentDidMount(). It sets state after 2.5 seconds to simulate calling a server to retrieve data. This example requests the current total active users for a site. In the render method, render the value of activeUsers in the h1. Watch what happens in the preview, and feel free to change the timeout to see the different effects
```
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      activeUsers: null
    };
  }
  componentDidMount() {
    setTimeout( () => {
      this.setState({
        activeUsers: 1273
      });
    }, 2500);
  }
  render() {
    return (
      <div>
        <h1>Active Users: { this.state.activeUsers }</h1>
      </div>
    );
  }
};

```

<div id="35b"/>

## Add Event Listeners

The componentDidMount() method is also the best place to attach any event listeners you need to add for specific functionality. React provides a synthetic event system which wraps the native event system present in browsers. This means that the synthetic event system behaves exactly the same regardless of the user's browser - even if the native events may behave differently between different browsers.

You've already been using some of these synthetic event handlers such as onClick(). React's synthetic event system is great to use for most interactions you'll manage on DOM elements. However, if you want to attach an event handler to the document or window objects, you have to do this directly.

Attach an event listener in the componentDidMount() method for keydown events and have these events trigger the callback handleKeyPress(). You can use document.addEventListener() which takes the event (in quotes) as the first argument and the callback as the second argument.

Then, in componentWillUnmount(), remove this same event listener. You can pass the same arguments to document.removeEventListener(). It's good practice to use this lifecycle method to do any clean up on React components before they are unmounted and destroyed. Removing event listeners is an example of one such clean up action.

```
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      message: ''
    };
    this.handleEnter = this.handleEnter.bind(this);
    this.handleKeyPress = this.handleKeyPress.bind(this);
  }
  // change code below this line
  componentDidMount() {
    document.addEventListener("keydown", this.handleKeyPress)
  }
  componentWillUnmount() {
    document.removeEventListener("keydown", this.handleKeyPress)
  }
  // change code above this line
  handleEnter() {
    this.setState({
      message: this.state.message + 'You pressed the enter key! '
    });
  }
  handleKeyPress(event) {
    if (event.keyCode === 13) {
      this.handleEnter();
    }
  }
  render() {
    return (
      <div>
        <h1>{this.state.message}</h1>
      </div>
    );
  }
};
```
**Resources**
[React Components](https://reactjs.org/docs/react-component.html)
[Common Lifecycles](http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)
[State and Lifecycles](https://reactjs.org/docs/state-and-lifecycle.html)
[document.addEventListener](https://www.w3schools.com/jsref/met_document_addeventlistener.asp)
[HTML DOM Events](https://www.w3schools.com/jsref/dom_obj_event.asp)


<div id="36b"/>

## Manage Updates with Lifecycle Methods

Another lifecycle method is componentWillReceiveProps() which is called whenever a component is receiving new props. This method receives the new props as an argument, which is usually written as nextProps. You can use this argument and compare with this.props and perform actions before the component updates. For example, you may call setState() locally before the update is processed.

Another method is componentDidUpdate(), and is called immediately after a component re-renders. Note that rendering and mounting are considered different things in the component lifecycle. When a page first loads, all components are mounted and this is where methods like componentWillMount() and componentDidMount() are called. After this, as state changes, components re-render themselves. The next challenge covers this in more detail.

The child component Dialog receives message props from its parent, the Controller component. Write the componentWillReceiveProps() method in the Dialog component and have it log this.props and nextProps to the console. You'll need to pass nextProps as an argument to this method and although it's possible to name it anything, name it nextProps here.

Next, add componentDidUpdate() in the Dialog component, and log a statement that says the component has updated. This method works similar to componentWillUpdate(), which is provided for you. Now click the button to change the message and watch your browser console. The order of the console statements show the order the methods are called.

Note: You'll need to write the lifecycle methods as normal functions and not as arrow functions to pass the tests (there is also no advantage to writing lifecycle methods as arrow functions).

**Manage Updates with Lifecycle Methods**

This challenge has you creating a couple lifecycle functions, componentWillUpdate and ComponentWillReceiveProps. You will be provided with another function called componentDidUpdate. We’ll discuss how you use them at each stage of the component lifecycle and why you should use them when you are checking different stages of your component.

Lets talk about the functions and how you will be using them. Component lifecycles can be broken down into 4 stages. Initlization -> Mounting -> Updating -> Unmounting. The components that you will work with are going to fall within the Updating stage.

The progression in which these functions are called are as follows: componentWillReceiveProps -> componentWillUpdate -> componentDidUpdate

When you create componentWillReceiveProps, this function will check to see if there are new props being received. If the component did receive new props then the function will be called and within the block you can compare the two prop states. The function will take in an argument typically named nextProps and will compare it to this.props. The challenge has you creating this function using the passed argument nextProps. See provided function below.

Next in the component lifecycle componentWillUpdate will be called, this function will check to see if there has been any updates to props or state and will be called before the component renders. The challenge has already provided you with this function and it logs out “Component is about to update.”

Once the component passes through the componentWillUpdate phase and the component renders, componentDidUpdate will be called. At this stage you can call this.setState to update any state chanegs that occurred during the first two phases. Note: you can only call setState if you wrap within a condition. Since this challenge only has you scratching the surface they would like you to log out that the “Component has updated.”

Once you have implemented all the lifecycle functions you should see some console logs being displayed. First, you will see componentWillReceiveProps send you this.props and nextProps. Next, you will see a console log letting you know that componentWillUpdate. Lastly, after the component renders it will call the componentDidUpdate and will log out “Component has updated.”

Note: The components that you are creating have been deprecated and will be available to use until version 17. You can find more information about these functions in the resource section below.
```
class Dialog extends React.Component {
  constructor(props) {
    super(props);
  }
  componentWillUpdate() {
    console.log('Component is about to update...');
  }
  // change code below this line
  
  // Create componentWillReceiveProps
  // Pass in argument nextProps and log out the current prop and next prop
  componentWillReceiveProps(nextProps) {
    // Log the current property and the next property  
    console.log(this.props, nextProps)
  }

  // Create function componentDidUpdate
  // Log out that the component has updated
  componentDidUpdate() {
    console.log("Component has updated")
  }
  
  // change code above this line
  render() {
    return <h1>{this.props.message}</h1>
  }
};

class Controller extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      message: 'First Message'
    };
    this.changeMessage = this.changeMessage.bind(this);
  }
  changeMessage() {
    this.setState({
      message: 'Second Message'
    });
  }
  render() {
    return (
      <div>
        <button onClick={this.changeMessage}>Update</button>
        <Dialog message={this.state.message}/>
      </div>
    );
  }
};
```
**Resources**
[React Component Lifecycle](https://reactjs.org/docs/react-component.html#the-component-lifecycle)
[React Component Lifecycle Visual](https://cdn-images-1.medium.com/max/2000/1*sn-ftowp0_VVRbeUAFECMA.png)


<div id="37b"/>

## Optimize Re-Renders with shouldComponentUpdate

So far, if any component receives new state or new props, it re-renders itself and all its children. This is usually okay. But React provides a lifecycle method you can call when child components receive new state or props, and declare specifically if the components should update or not. The method is shouldComponentUpdate(), and it takes nextProps and nextState as parameters.

This method is a useful way to optimize performance. For example, the default behavior is that your component re-renders when it receives new props, even if the props haven't changed. You can use shouldComponentUpdate() to prevent this by comparing the props. The method must return a boolean value that tells React whether or not to update the component. You can compare the current props (this.props) to the next props (nextProps) to determine if you need to update or not, and return true or false accordingly.

The shouldComponentUpdate() method is added in a component called OnlyEvens. Currently, this method returns true so OnlyEvens re-renders every time it receives new props. Modify the method so OnlyEvens updates only if the value of its new props is even. Click the Add button and watch the order of events in your browser's console as the other lifecycle hooks are triggered.

For this solution, you will use an if/then statement to check whether the value of nextProps is even. nextProps differs from props in that it is a value that has not been rendered in the UI yet so in the shouldComponentUpdate() method, you are essentially asking permission to update the UI with the nextProps value.
```
class OnlyEvens extends React.Component {
  constructor(props) {
    super(props);
  }
  shouldComponentUpdate(nextProps, nextState) {
    console.log('Should I update?');
     // change code below this line
    if (nextProps.value % 2 == 0) {
        return true;
      }
      return false;
     // change code above this line
  }
  componentWillReceiveProps(nextProps) {
    console.log('Receiving new props...');
  }
  componentDidUpdate() {
    console.log('Component re-rendered.');
  }
  render() {
    return <h1>{this.props.value}</h1>
  }
};

class Controller extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: 0
    };
    this.addValue = this.addValue.bind(this);
  }
  addValue() {
    this.setState({
      value: this.state.value + 1
    });
  }
  render() {
    return (
      <div>
        <button onClick={this.addValue}>Add</button>
        <OnlyEvens value={this.state.value}/>
      </div>
    );
  }
};

```

<div id="38b"/>

## Introducing Inline Styles

There are other complex concepts that add powerful capabilities to your React code. But you may be wondering about the more simple problem of how to style those JSX elements you create in React. You likely know that it won't be exactly the same as working with HTML because of the way you apply classes to JSX elements.

If you import styles from a stylesheet, it isn't much different at all. You apply a class to your JSX element using the className attribute, and apply styles to the class in your stylesheet. Another option is to apply inline styles, which are very common in ReactJS development.

You apply inline styles to JSX elements similar to how you do it in HTML, but with a few JSX differences. Here's an example of an inline style in HTML:
```
<div style="color: yellow; font-size: 16px">Mellow Yellow</div>
```
JSX elements use the style attribute, but because of the way JSX is transpiled, you can't set the value to a string. Instead, you set it equal to a JavaScript object. Here's an example:
```
<div style={{color: "yellow, fontSize: 16}}>Mellow Yellow</div>
```
Notice how we camelCase the "fontSize" property? This is because React will not accept kebab-case keys in the style object. React will apply the correct property name for us in the HTML.

Add a style attribute to the div in the code editor to give the text a color of red and font size of 72px.

Note that you can optionally set the font size to be a number, omitting the units "px", or write it as "72px".
```
class Colorful extends React.Component {
  render() {
    return (
      <div style={{color: "red", fontSize: "72px"}}>Big Red</div>
    );
  }
};
```

<div id="39b"/>

## Add Inline Styles in React

You may have noticed in the last challenge that there were several other syntax differences from HTML inline styles in addition to the style attribute set to a JavaScript object. First, the names of certain CSS style properties use camel case. For example, the last challenge set the size of the font with fontSize instead of font-size. Hyphenated words like font-size are invalid syntax for JavaScript object properties, so React uses camel case. As a rule, any hyphenated style properties are written using camel case in JSX.

All property value length units (like height, width, and fontSize) are assumed to be in px unless otherwise specified. If you want to use em, for example, you wrap the value and the units in quotes, like {fontSize: "4em"}. Other than the length values that default to px, all other property values should be wrapped in quotes.

If you have a large set of styles, you can assign a style object to a constant to keep your code organized. Uncomment the styles constant and declare an object with three style properties and their values. Give the div a color of "purple", a font-size of 40, and a border of "2px solid purple". Then set the style attribute equal to the styles constant.
```
const styles = {
   color: "purple",
   fontSize: 40,
   border: "2px solid purple"
 };
// change code above this line
class Colorful extends React.Component {
  render() {
    // change code below this line
    return (
      <div style={styles}>Style Me!</div>
    );
    // change code above this line
  }
};
```

<div id="40b"/>

## Use Advanced JavaScript in React Render Method

In previous challenges, you learned how to inject JavaScript code into JSX code using curly braces, { }, for tasks like accessing props, passing props, accessing state, inserting comments into your code, and most recently, styling your components. These are all common use cases to put JavaScript in JSX, but they aren't the only way that you can utilize JavaScript code in your React components.

You can also write JavaScript directly in your render methods, before the return statement, without inserting it inside of curly braces. This is because it is not yet within the JSX code. When you want to use a variable later in the JSX code inside the return statement, you place the variable name inside curly braces.

In the code provided, the render method has an array that contains 20 phrases to represent the answers found in the classic 1980's Magic Eight Ball toy. The button click event is bound to the ask method, so each time the button is clicked a random number will be generated and stored as the randomIndex in state. On line 52, delete the string "change me!" and reassign the answer const so your code randomly accesses a different index of the possibleAnswers array each time the component updates. Finally, insert the answer const inside the p tags.
While you are inside the render method and not inside the return method, you can write JavaScript without wrapping it inside curly braces.

First, you will have to set the constant ‘answer’ to a value. Access the ‘possibleAnswers’ array using the value of ‘randomIndex’, which is located within the state of your component. Remember, you access state using this.state.
Next, insert your const ‘answer’ into the p-tags. Make sure to wrap it with curly braces { }.
```
const inputStyle = {
  width: 235,
  margin: 5
}

class MagicEightBall extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      userInput: '',
      randomIndex: ''
    }
    this.ask = this.ask.bind(this);
    this.handleChange = this.handleChange.bind(this);
  }
  ask() {
    if (this.state.userInput) {
      this.setState({
        randomIndex: Math.floor(Math.random() * 20),
        userInput: ''
      });
    }
  }
  handleChange(event) {
    this.setState({
      userInput: event.target.value
    });
  }
  render() {
    const possibleAnswers = [
      'It is certain',
      'It is decidedly so',
      'Without a doubt', 
      'Yes, definitely',
      'You may rely on it',
      'As I see it, yes',
      'Outlook good',
      'Yes',
      'Signs point to yes',
      'Reply hazy try again',
      'Ask again later',
      'Better not tell you now',
      'Cannot predict now',
      'Concentrate and ask again',
      'Don\'t count on it', 
      'My reply is no',
      'My sources say no',
      'Most likely',
      'Outlook not so good',
      'Very doubtful'
    ];
    const answer = possibleAnswers[this.state.randomIndex]; // << change code here
    return (
      <div>
        <input
          type="text"
          value={this.state.userInput}
          onChange={this.handleChange}
          style={inputStyle} /><br />
        <button onClick={this.ask}>
          Ask the Magic Eight Ball!
        </button><br />
        <h3>Answer:</h3>
        <p>
          { /* change code below this line */ }
          {answer}
          { /* change code above this line */ }
        </p>
      </div>
    );
  }
};
```



<div id="41b"/>

## Render with an If/Else Condition

Another application of using JavaScript to control your rendered view is to tie the elements that are rendered to a condition. When the condition is true, one view renders. When it's false, it's a different view. You can do this with a standard if/else statement in the render() method of a React component.

MyComponent contains a boolean in its state which tracks whether you want to display some element in the UI or not. The button toggles the state of this value. Currently, it renders the same UI every time. Rewrite the render() method with an if/else statement so that if display is true, you return the current markup. Otherwise, return the markup without the h1 element.

Note: You must write an if/else to pass the tests. Use of the ternary operator will not pass here.
```
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      display: true
    }
    this.toggleDisplay = this.toggleDisplay.bind(this);
  }
  toggleDisplay() {
    this.setState({
      display: !this.state.display
    });
  }
  render() {
    // change code below this line
    if (this.state.display) {
      return (
        <div>
         <button onClick={this.toggleDisplay}>Toggle Display</button>
         <h1>Displayed!</h1>
       </div>
      );
    } else {
      return (
        <div>
         <button onClick={this.toggleDisplay}>Toggle Display</button>
       </div>
      );
    }
  }
};
```

<div id="42b"/>

## Use && for a More Concise Conditional

The if/else statements worked in the last challenge, but there's a more concise way to achieve the same result. Imagine that you are tracking several conditions in a component and you want different elements to render depending on each of these conditions. If you write a lot of else if statements to return slightly different UIs, you may repeat code which leaves room for error. Instead, you can use the && logical operator to perform conditional logic in a more concise way. This is possible because you want to check if a condition is true, and if it is, return some markup. Here's an example:
```
{condition && <p>markup</p>}
```
If the condition is true, the markup will be returned. If the condition is false, the operation will immediately return false after evaluating the condition and return nothing. You can include these statements directly in your JSX and string multiple conditions together by writing && after each one. This allows you to handle more complex conditional logic in your render() method without repeating a lot of code.

Solve the previous example again, so the h1 only renders if display is true, but use the && logical operator instead of an if/else statement.
```
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      display: true
    }
    this.toggleDisplay = this.toggleDisplay.bind(this);
  }
  toggleDisplay() {
    this.setState({
      display: !this.state.display
    });
  }
  render() {
    // change code below this line
    return (
       <div>
         <button onClick={this.toggleDisplay}>Toggle Display</button>
         {this.state.display && <h1>Displayed!</h1>}
       </div>
    );
  }
};
```


<div id="43b"/>

## Use a Ternary Expression for Conditional Rendering

Before moving on to dynamic rendering techniques, there's one last way to use built-in JavaScript conditionals to render what you want: the ternary operator. The ternary operator is often utilized as a shortcut for if/else statements in JavaScript. They're not quite as robust as traditional if/else statements, but they are very popular among React developers. One reason for this is because of how JSX is compiled, if/else statements can't be inserted directly into JSX code. You might have noticed this a couple challenges ago — when an if/else statement was required, it was always outside the return statement. Ternary expressions can be an excellent alternative if you want to implement conditional logic within your JSX. Recall that a ternary operator has three parts, but you can combine several ternary expressions together. Here's the basic syntax:
```
condition ? expressionIfTrue : expressionIfFalse
```
The code editor has three constants defined within the CheckUserAge component's render() method. They are called buttonOne, buttonTwo, and buttonThree. Each of these is assigned a simple JSX expression representing a button element. First, initialize the state of CheckUserAge with input and userAge both set to values of an empty string.

Once the component is rendering information to the page, users should have a way to interact with it. Within the component's return statement, set up a ternary expression that implements the following logic: when the page first loads, render the submit button, buttonOne, to the page. Then, when a user enters their age and clicks the button, render a different button based on the age. If a user enters a number less than 18, render buttonThree. If a user enters a number greater than or equal to 18, render buttonTwo.
```

const inputStyle = {
  width: 235,
  margin: 5
}

class CheckUserAge extends React.Component {
  constructor(props) {
    super(props);
    // change code below this line

    // change code above this line
    this.submit = this.submit.bind(this);
    this.handleChange = this.handleChange.bind(this);
  }
  handleChange(e) {
    this.setState({
      input: e.target.value,
      userAge: ''
    });
  }
  submit() {
    this.setState({
      userAge: this.state.input
    });
  }
  render() {
    const buttonOne = <button onClick={this.submit}>Submit</button>;
    const buttonTwo = <button>You May Enter</button>;
    const buttonThree = <button>You Shall Not Pass</button>;
    return (
      <div>
        <h3>Enter Your Age to Continue</h3>
        <input
          style={inputStyle}
          type="number"
          value={this.state.input}
          onChange={this.handleChange} /><br />
        {
          /* change code here */
        }
      </div>
    );
  }
};
```
Ternary operator has three parts, but you can combine several ternary expressions together. Here’s the basic syntax:
```
condition ? expressionIfTrue : expressionIfFalse
```
Here is sample solution of using ternary expression. First you need declare state in constructor like this
```
constructor(props) {
    super(props);
    // change code below this line
      this.state = {
        input: '',
        userAge: ''
      }
    // change code above this line
    this.submit = this.submit.bind(this);
    this.handleChange = this.handleChange.bind(this);
  }
```
Then the ternary operator 
```
{
    /* change code here */
    (this.state.userAge >= 18) ? buttonTwo : (this.state.userAge== '')? buttonOne: buttonThree

}
```


<div id="44b"/>

## Render Conditionally from Props

So far, you've seen how to use if/else, &&, null and the ternary operator (condition ? expressionIfTrue : expressionIfFalse) to make conditional decisions about what to render and when. However, there's one important topic left to discuss that lets you combine any or all of these concepts with another powerful React feature: props. Using props to conditionally render code is very common with React developers — that is, they use the value of a given prop to automatically make decisions about what to render.

In this challenge, you'll set up a child component to make rendering decisions based on props. You'll also use the ternary operator, but you can see how several of the other concepts that were covered in the last few challenges might be just as useful in this context.

The code editor has two components that are partially defined for you: a parent called GameOfChance, and a child called Results. They are used to create a simple game where the user presses a button to see if they win or lose.

First, you'll need a simple expression that randomly returns a different value every time it is run. You can use Math.random(). This method returns a value between 0 (inclusive) and 1 (exclusive) each time it is called. So for 50/50 odds, use Math.random() > .5 in your expression. Statistically speaking, this expression will return true 50% of the time, and false the other 50%. On line 30, replace the comment with this expression to complete the variable declaration.

Now you have an expression that you can use to make a randomized decision in the code. Next you need to implement this. Render the Results component as a child of GameOfChance, and pass in expression as a prop called fiftyFifty. In the Results component, write a ternary expression to render the text "You win!" or "You lose!" based on the fiftyFifty prop that's being passed in from GameOfChance. Finally, make sure the handleClick() method is correctly counting each turn so the user knows how many times they've played. This also serves to let the user know the component has actually updated in case they win or lose twice in a row.
```
class Results extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <h1>
      {
        this.props.fiftyFifty
      }
      </h1>
    )
  };
};

class GameOfChance extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      counter: 1
    }
    this.handleClick = this.handleClick.bind(this);
  }
  handleClick() {
    this.setState({
      counter: this.state.counter +1 // change code here
    });
  }
  render() {
    let expression = Math.random() > .5; // change code here
    return (
      <div>
        <button onClick={this.handleClick}>Play Again</button>
        { /* change code below this line */ }
        {(expression == 1) ? <Results fiftyFifty="You win!"/> : <Results fiftyFifty="You lose!" />}
        { /* change code above this line */ }
        <p>{'Turn: ' + this.state.counter}</p>
      </div>
    );
  }
};
```
Change handleClick() with proper increament statement.
```
handleClick() {
  this.setState({
    counter: this.state.counter + 1
  });
}
```
In render() method use Math.random() as mentioned in the challenge description and write a ternary expression to pass props in the Results component.
```
 let expression = Math.random() > .5;
    
{(expression == 1)? <Results fiftyFifty="You win!"/> : <Results fiftyFifty="You lose!"/> }
```
Then render the fiftyFifty props in the Results component.
```
<h1>
  {
    this.props.fiftyFifty
  }
  </h1>
```

<div id="45b"/>

## Change Inline CSS Conditionally Based on Component State

At this point, you've seen several applications of conditional rendering and the use of inline styles. Here's one more example that combines both of these topics. You can also render CSS conditionally based on the state of a React component. To do this, you check for a condition, and if that condition is met, you modify the styles object that's assigned to the JSX elements in the render method.

This paradigm is important to understand because it is a dramatic shift from the more traditional approach of applying styles by modifying DOM elements directly (which is very common with jQuery, for example). In that approach, you must keep track of when elements change and also handle the actual manipulation directly. It can become difficult to keep track of changes, potentially making your UI unpredictable. When you set a style object based on a condition, you describe how the UI should look as a function of the application's state. There is a clear flow of information that only moves in one direction. This is the preferred method when writing applications with React.

The code editor has a simple controlled input component with a styled border. You want to style this border red if the user types more than 15 characters of text in the input box. Add a condition to check for this and, if the condition is valid, set the input border style to 3px solid red. You can try it out by entering text in the input.

You are going to be checking the length of this.state.input so use it’s .length property
```
this.state.input.length
```
You are entering code before the return statement so you can use a pure JavaScript if/then statement.
```
class GateKeeper extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      input: ''
    };
    this.handleChange = this.handleChange.bind(this);
  }
  handleChange(event) {
    this.setState({ input: event.target.value })
  }
  render() {
    let inputStyle = {
      border: '1px solid black'
    };
    // change code below this line
    if (this.state.input.length > 15) {
      inputStyle.border = '3px solid red';
    }

    // change code above this line
    return (
      <div>
        <h3>Don't Type Too Much:</h3>
        <input
          type="text"
          style={inputStyle}
          value={this.state.input}
          onChange={this.handleChange} />
      </div>
    );
  }
};
```
You will use an if/then statement to check the value of this.state.input.length. If it is longer than 15, assign '3px solid red' to inputStyle.border.
Write a conditional statement that is evaluated according to your state, as mentioned in the challenge description, checks the length of the input and assigns a new object to the inputStyle variable.
```
if (this.state.input.length > 15) {
  inputStyle = {
    border: '3px solid red'
  }
}
```

<div id="46b"/>

## Use Array.map() to Dynamically Render Elements

Conditional rendering is useful, but you may need your components to render an unknown number of elements. Often in reactive programming, a programmer has no way to know what the state of an application is until runtime, because so much depends on a user's interaction with that program. Programmers need to write their code to correctly handle that unknown state ahead of time. Using Array.map() in React illustrates this concept.

For example, you create a simple "To Do List" app. As the programmer, you have no way of knowing how many items a user might have on their list. You need to set up your component to dynamically render the correct number of list elements long before someone using the program decides that today is laundry day. 

```
const textAreaStyles = {
  width: 235,
  margin: 5
};

class MyToDoList extends React.Component {
  constructor(props) {
    super(props);
    // change code below this line
    this.state = {
      userInput: '',
      toDoList: []
    }
    // change code above this line
    this.handleSubmit = this.handleSubmit.bind(this);
    this.handleChange = this.handleChange.bind(this);
  }
  handleSubmit() {
    const itemsArray = this.state.userInput.split(',');
    this.setState({
      toDoList: itemsArray
    });
  }
  handleChange(e) {
    this.setState({
      userInput: e.target.value
    });
  }
  render() {
    const items = this.state.toDoList.map((item)=> <li>{item}</li>);
    return (
      <div>
        <textarea
          onChange={this.handleChange}
          value={this.state.userInput}
          style={textAreaStyles}
          placeholder="Separate Items With Commas" /><br />
        <button onClick={this.handleSubmit}>Create List</button>
        <h1>My "To Do" List:</h1>
        <ul>
          {items}
        </ul>
      </div>
    );
  }
};
```

<div id="47b"/>

## Give Sibling Elements a Unique Key Attribute

The last challenge showed how the map method is used to dynamically render a number of elements based on user input. However, there was an important piece missing from that example. When you create an array of elements, each one needs a key attribute set to a unique value. React uses these keys to keep track of which items are added, changed, or removed. This helps make the re-rendering process more efficient when the list is modified in any way. Note that keys only need to be unique between sibling elements, they don't need to be globally unique in your application.

The code editor has an array with some front end frameworks and a stateless functional component named Frameworks(). Frameworks() needs to map the array to an unordered list, much like in the last challenge. Finish writing the map callback to return an li element for each framework in the frontEndFrameworks array. This time, make sure to give each li a key attribute, set to a unique value.

Normally, you want to make the key something that uniquely identifies the element being rendered. As a last resort the array index may be used, but typically you should try to use a unique identification.
```
const frontEndFrameworks = [
  'React',
  'Angular',
  'Ember',
  'Knockout',
  'Backbone',
  'Vue'
];

function Frameworks() {
  // Just add key attribute to the <li> tag to make unique 
  const renderFrameworks = frontEndFrameworks.map((item) => <li key={item+1}>{item}</li>);
  return (
    <div>
      <h1>Popular Front End JavaScript Frameworks</h1>
      <ul>
        {renderFrameworks}
      </ul>
    </div>
  );
};
```

<div id="48b"/>

## Use Array.filter() to Dynamically Filter an Array

The map array method is a powerful tool that you will use often when working with React. Another method related to map is filter, which filters the contents of an array based on a condition, then returns a new array. For example, if you have an array of users that all have a property online which can be set to true or false, you can filter only those users that are online by writing:
```
let onlineUsers = users.filter(user => user.online);
```
In the code editor, MyComponent's state is initialized with an array of users. Some users are online and some aren't. Filter the array so you see only the users who are online. To do this, first use filter to return a new array containing only the users whose online property is true. Then, in the renderOnline variable, map over the filtered array, and return a li element for each user that contains the text of their username. Be sure to include a unique key as well, like in the last challenges.
Use .filter() to create a new array that only shows users online.
```
this.state.users.filter(i => i.online == true)
```
Use .map() from previous the previous exercise to list out the online users and give them a unique key.
```
usersOnline.map((i) => <li key={i.username + 1}>{i.username}</li>)
```
Both methods combined will first filter out the array, then list them individually.
```
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      users: [
        {
          username: 'Jeff',
          online: true
        },
        {
          username: 'Alan',
          online: false
        },
        {
          username: 'Mary',
          online: true
        },
        {
          username: 'Jim',
          online: false
        },
        {
          username: 'Sara',
          online: true
        },
        {
          username: 'Laura',
          online: true
        }
      ]
    }
  }
  render() {
    const usersOnline = this.state.users.filter(i => i.online == true); // change code here
    const renderOnline = usersOnline.map((i) => <li key={i.username + 1}>{i.username}</li>); // change code here
    return (
       <div>
         <h1>Current Online Users:</h1>
         <ul>
           {renderOnline}
         </ul>
       </div>
    );
  }
};
```

<div id="49b"/>

## Render React on the Server with renderToString

So far, you have been rendering React components on the client. Normally, this is what you will always do. However, there are some use cases where it makes sense to render a React component on the server. Since React is a JavaScript view library and you can run JavaScript on the server with Node, this is possible. In fact, React provides a renderToString() method you can use for this purpose.

There are two key reasons why rendering on the server may be used in a real world app. First, without doing this, your React apps would consist of a relatively empty HTML file and a large bundle of JavaScript when it's initially loaded to the browser. This may not be ideal for search engines that are trying to index the content of your pages so people can find you. If you render the initial HTML markup on the server and send this to the client, the initial page load contains all of the page's markup which can be crawled by search engines. Second, this creates a faster initial page load experience because the rendered HTML is smaller than the JavaScript code of the entire app. React will still be able to recognize your app and manage it after the initial load.

The renderToString() method is provided on ReactDOMServer, which is available here as a global object. The method takes one argument which is a React element. Use this to render App to a string.
You pass a class to .renderToString() just like you would pass a component to a render method.
```
class App extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return <div/>
  }
};

// change code below this line
ReactDOMServer.renderToString(<App />);
```


