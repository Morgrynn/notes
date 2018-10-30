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

---


<div id="debugging"/>

## Debugging 

Table of Contents
1. [Intro to the Debugging Challanges](#1)
2. [Use typeof to Check the Type of a Variable](#2)
3. [Catching Misspelled Variable and Function Names](#3)
4. [Catch Unclosed Parentheses, Brackets, Braces and Quotes](#4)
5. [Catch Mixed Usage of Single and Double Quotes](#5)
6. [Catch Use of Assignment Operator Instead of Equality Operator](#6)
7. [Catch Missing Open and Closing Parenthesis After a Function Call](#7)
8. [Catch Off By One Errors When Using Indexing](#8)
9. [Use Caution When Reinitializing Variables Inside a Loop](#9)
10. [Prevent Infinite Loops with a Valid Terminal Condition](#10)

<div id="1"/>

### Intro to the Debugging Challenges

Debugging is the process of finding exactly what isn't working and fixing it.
These issues generally come in three forms:

1. syntax errors that prevent a program from running.
2. runtime errors when code fails to execute or has unexpected behaviour.
3. semantic (or logical) errors when code does'nt do what it's meant to.

Example of syntax error - often detected by the code editor:

```
funtion willNotWork({
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
// Calling loopy starts an infinite loop, whic may crash your browser
```

Example of a semantic error - often detected after testing code output:

```
function calcAreaOfRect(w,h) {
    return w + h; // This should be w * h
}
let myRectArea = calcAreaOfRect(2,3);
// Correct syntax and the program executes, but this gives the wrong answer
```

Debugging is frustrating but it helps to develop (and follow) a **step-by-step** approach to review your code.
This means checking the intermediate values and types of variables to see if they are what they should be.
You can start with simple process of elimination.

For example, if function A works and returns what its supposed to, the function B may have the issue. 
Or start checking values in a block of code from the middle to try to cut the search space in half. 
A problem in one spot indicates a bug in the first half of the code. If not, it's likely in the second.

This section will cover a couple helpful tools to find bugs, and some of the common forms the take.
Fortunatley, debugging is a learnable skill that just requires a little patience and practice to master.


<div id="2"/>

### Use typeof to Check the Type of a Variable

You can use typeof to check the data structure, or type, of a variable. This is userful in debugging when working with multiple data types. If you can think you're adding two numbers, but one is actually a string, the results can be unexpected. Type errors can lurk in calculations or function calls. Be careful when you're accessing and working with external data in the form of a JavaScript Object Notation(JSON) object.

Here's are some examples using typeof:

```
console.log(typeof ""): // oputputs "string"
console.log(typeof 0): // oputputs "number"
console.log(typeof []): // oputputs "object"
console.log(typeof {}): // oputputs "object"

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

The console.log() and typeof methods are the two primary ways to check intermediate values and types of program output. Now it's time to get into the common forms that bugs take. One syntax-level issue that fast typers can commiserate with is the humble spelling error.

Transposed, missing, or mis-capitalized characters in a variable or function name will have the brower looking for an object that doesn't exist - and complain in the form of a reference error. JavaScript variable and function names are case-sensitive.

Fix the two spelling errors in the code so the netWorkingCapital calculation works.

```
let receivables = 10;
let payables = 8;
let netWorkingCapital = recievables - payable;
console.log(`Net working capital is: ${netWorkingCapital}`);
```

<div id="4"/>

### Catch Unclosed Parentheses, Brackets, Braces and Quotes

Another syntax error to be aware of is that all opening parentheses, brackets, curly braces, and quotes have a closing pair. Forgetting a peice tends to happen when you're editing existing code and inserting items with one of the pair types. Also, take care when nesting code blocks into others, such as adding a callback function as an argument to a method.

One way to avoid this mistake is as soon as the opening character is typed, immediately include the closing match, then move the curser back between them ans continue coding. Fortunately, most mordern code editors generate the second haöf of the pair automatically.


<div id="5"/>

### Catch Mixed Usage of Single and Double Quotes

JavaScript allows the use of both single('') and double("") quotes to declare a string. Deciding which one to use generally comes down to personal prefernce, with some exceptions.
Having two choices is great when a string has contractions or another piece of text that's in quotes. just be careful that you don't close the string too early, which causes a syntax error.

Here are some examples of mixing quotes:

```
// These are correct:
const grouchoContraction = "I've had a perfectly wonderful evening, but this wasn't it.";
const quoteInString = "Groucho Marx once said 'Quote me as saying I was mis-quoted.'";
//This is incorrect:
const uhOhGroucho = 'I've had a perfectly wonderful evening, but this wasn't it.';
```

Of course, it is okay to use onöy one style of quotes. You can escape the quotes inside the string by using the backslash (\) escape character:

```
// Correct use of same quotes:
const allSameQuotes = 'I\'ve had a perfectly wonderful evening, but this wasn\'t it.';
```

<div id="6"/>

### Catch Use of Assignment Operator Instead of Equality Operator

Branching programs, i.e. ones that do different things if certain conditions are met, rely on if, else if, and else statements in JavaScript. The condition sometimes takes the form of testing whether a result is equal to a value.
The logic is spoken (in English, at least) as "if x equals y, then ..." which can literally translate into code using the =, or assignment operator. This leads to unexpected control flow in your program.

As covered in previous challenges, the assingment operator(=) in JavaScript assigns a value to a variable name. And the == and === operators check for equality (the triple === tests for stict equality, meaning both value and type are the same).

The cose below assigns x to be 2, which evaluates as true. Almost every value on its own in JavaScript evaluates to true, except what are known as "falsy" values: false, 0, "" (an empty string), NaN, undefined, and null.

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

**Off by one error** (sometimes called OBOE) crop up when you're tryng to target a specific index of a string or array (to slice or access a segment), or when looping over the indices of them. JavaScript indexing starts at zero, not one, ehich means the last index is always one less than the length of the item. If you try to access an index equal to the length, the program may throw an "index out of range" reference error or print undefined.

When you use string or array methods that take index ranges as arguments, it helps to read the documentation and unerstand  if they are inclusive (the item at the given index is part of what's returned) or not. Here are some examples of off by one errors.

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

### Use Caution When Reinitializing Variables Inside a Loop

Sometimes it's necessary to save information, increment counters, or re-set variables within a loop. A potential issue is when variables either should be reinitialized, and aren't, or vice versa. This is particularly dangerous if you accidentally reset the variable being used for the terminal condition, causing an infinite loop.

Printing variable values with each cycle of your loop by using console.log() can uncover buggy behaviour related to resetting, or failing to reset a variable.

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
      Now a new row will be initialised during each iteration of the outer loop allowing 
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

The myFunc() function constains an infinite loop because the terminal condition i != 4 will never evaluate to false (and break the looping) -i will increment by 2 each pass, and jump right over 4 since i is odd to start. Fix the comparison operator in the terminal condition so the loop only runs for i less than or equal to 4.

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

The below is an example of the simplest implementation of an array data structure. This is known as a _one-dimensional array_, meaning it only has one level, or that it does not have any other arrays nested within it. Notice it contains _booleans, strings and numbers_, amoung other valid JavaScript data types:

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

An array's length, like the data types it can contain, is not fixed. Arrays can be defned with a length of any number of elements, and elements can be added or removed over time;in other words, arrays are _mutable_. In this challenge, we will look at two methods with which we can programmatically modify an array: Array.push() and Array.unshift().

Both methods taek one or more elements as parameters and add those elements to the array the method is being called on; the push() method adds elements to the end of an array, and unshift() adds elements to the beginning.
consider the following: 

```
let twentyThree = 'XXIII';
let romanNumerals = ['XXI', 'XXII'];

romanNumerals.unshift('XIX', 'XX');
// now equals ['XIX', 'XX', 'XXI', 'XXII']

romanNumerals.push(twentyThree);
// now equals ['XIX', 'XX', 'XXI', 'XXII', 'XXIII']
```
Notice that we can also pass variables, which allows us even greater flexibilty in dynamically modifying our array's data.

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
We can also return the value of the removed elemet with either method like this:
```
let popped = greetings.pop();
// returns 'hello'
// greetings now equals []

```

<div id="id-section6"/>

### Remove Items Using splice()

Ok, so we've learned how to remove elements from the beginning and end of arrays using shift() and pop(), but what if we want to remove an element from somewhere in the middle? Or remove more than one element at once? Well, that's where splice() comes in. splice() allows us to do just that: **remove any number of consecutive elements** from anywhere in an array.

splice() can take up to 3 parameters, but for now, we'll focus on just the first 2. The first two parameters of splice() are integers which represent indexes, or positions, of the array that splice() is being called upon. And remember, arrays are _zero-indexed_, so to indecate the first-element of an array, we would use 0. splice()'s first parameter represents the index on the array from which to begin removing elements, while the second parameter indicates the number of elements to delete.For example:

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

While slice() allows us to be selective about what elements of an array to copy, amoung several other useful tasks, ES6's _new spread operator_ allows us to easily copy _all_ of an array's elements, in order, with a simple and highly readable syntax. The spread syntax looks like this: ...

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

Sometimes when working with arrays, it is very handy to be able to iterate throught each item to find one or more elements that we might need, or to manipulate an array based on which data items meet a certain set of criteria. JavaScript offers several built in methods that each iterate over arrays in slightly different ways to achieve different results (such as **every(), forEach(), map(), etc**), however the technique which is most flexible and offers us the greatest amount of control is a simple for loop.

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
  ampletedProjects: 15
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
nestedObjects has three unique keys: id, whise value is a number, date whose value is a string, and data, whose value is an object which has yet another object nested within it. While structures can quickly become complex, we can still use the same notations to access the information we need.

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
Simply define the object and then use dot-notation to access the second object and finally the final element you widh to modify.

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
  * The simplest way to complete this challenge is to create an if-statement to check wether or not the object contains all users, then to return a true or flase statement. The first solution does just this.
  * The second solution works in exactly the same way, only it uses 1 line of code - Conditional(ternary)-Operator - wihtin the function.

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

As its name implies, object oriented programming organizes code into object definitions. These are sometimes called classes, and they group together data with related behaviour. The data is an object's attibutes, and the behaviour (or functions) are methods.

The object structure makes it flexible within a program. Objects can transfer information by calling and passing data to another object's methods. Also, new classes can receive, or inherit, all the features from a base or parent class. This helps to reduce repeated code.

Your choice of programming approach depends on a few factors. These include the type of problem, as well as how you want to structure your data and algorithms. This section covers object oriented programming principles in JavaScript.

<div id="id-2"/>

### Create a Basic JavaScript Object

Think about things people see everyday, like cars, shops, and birds. These are all objects: tangible things people can observe and interact with.

What are some qualities of these objects? A car has wheels. Shops seel items. Birds have wings.

These qualities or properties, define what makes up an object. Note that similar objects share the same properties, but may have different values for those properties. For example, all cars have wheels, but not all cars have the same number of wheels.

Objects in JavaScript are used to model real-world objects, giiving them properties and behavior just like their real-world counterparts. Here's an example using these concepts to create a duck object:

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
    sayName: fucntion() {return "The name of this duck is " + duck.name + ".";}
};
duck.sayName();
// Returns "The name of this duck is Aflac
```

This example adds the sayName method, which is a function that returns a sentence giving the name of the duck.
Notice that the method accessed the name property in the return statement using duck.name. The next challenge will cover another way to do this.

<div id="id-5"/>

### Make Code More Reusable with the this Keyword

While the above example is a valid way to access the object's property, there is a pitfall here. If the variable name changes, any code referncing the original name would need to be updated as well. In a short object definition, it isn't a problem, but if an object has many references to its properties there is a greater chance for error.

A way to avoid these issues is with the this keyword:
```
let duck = {
    name: "Aflac",
    numLegs: 2,
    sayName: function() {return "The naem of this dick is " + this.name + ".";}
};
```

this is a deep topic, and the above example is only one way to use it. In the current context, this refers to the object that the method is assoiciated with: duck.

If the object's name is changed to mallard, it is not necessary to find all the references to duck in the code. It makes the code reusable and easier to read.

<div id="id-6"/>

### Define a Constructor Function

Constructors are functions that create new objects. They define properties and behaviors that will belong to the new object. Think of them as a blueprint for the creation of new objects.

Here is an example of a constructor:
```
functio Bird() {
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
Suppose you were writing a program to keep track of hundreds or even thousands of different birds in an aviary. It would take a lot of time to create all the birds, then change the properties to different calues for every one.

To more easily create different Bird objects, you can design your Bird constructor to accept parameters:
```
function Bird(name, color) {
    this.name = name;
    this.color = color;
    this.numLegs = 2;
}
```
Then pass in the values as arguments to define wach unique bird into the Bird constructor:

```
let cardinal = new Bird("Bruce", "red");
```
This gives a new instance of Bird with name and color properties set to Bruce and red, respectively. The numLegs property is still set to 2.

The cardianal has these properties:
```
cardinal.name // Bruce
cardinal.color // red
cardinal.numLegs // 2
```

The constructor is more flexible. It's now possible to define the properties for each Bird at the time it is created, which is one way that JavaScript constructors are so useful. They group objects together based on shared characteristics and behavior and define a blueprint that automates their creation.

<div id="id-9"/>

### Verify an Object's Constructor with instanceof

Anytime a constructor function createsw a new object, that object is said to be an instance of its constructor. JavaScript gives a convienient way to verify this with the instanceof operator. instanceof allows you to compare an object to a constructor, returning true or false based on whether or not that object was created with the constructor. Here's an example:

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

name and numLegs are called own properties, because they are defined directly on the instance object. That means that duck and canary each has its own seperate copy of these properties. 

In fact every instance of Bird will hace its own copy of these properties.

The following code adds all of the own properties of duck to the array ownProps:
```
let ownProps = [];

for (let property in duck) {
    if (duck.hasOwnProperty(property)) {
        ownProps.push(property);
    }
}

console.log(ownProps); // pronts ["name", "numLegs"]
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

Note that the prototype for duck and canary is part of the Bird constructor as Bird.prototype. Nearly ecery object in JavaScript has a prototype property which is part of the constructor function that created it.

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

Write a joinDogFraternity funciton that takes a candidate parameter and, using the constructor property, return true id the candidate is a Dog, otherwise return false.

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
A more efficent way is to set the prototype to a new object that already contains the properties. This way, the properties are added all at once:
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

The describe method is repeated in two places. The code can be edited to follow the DRY pronciple by creating a supertype(or parent) called Animal:

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

The eat method is repeated in both Cat and Bear. Edit th ecode in the spirit of DRY by moving the eat method to the Animal supertype.

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
This and the next challenge will cover hwo to reuse Animal's methods inside Bird and Dog without defining them aagin. It uses a technique called inheritance.

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

Object.create(obj) creates a new object, and sets obj as the new object's prototype. Recall that the prorotype is like the "recipe" for creating an object. By setting the prototype of animal to be Animal's prototype, you are effectivaely giving the animal instance the same "recipe" as any other instance of Animal.

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

Rmemeber that the prototype is like the "recipe" for creating an object. In a way, the recipe for Bird now includes all the key "ingrediants" from Animal.

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

In the previous challenge, bird had a public property name. It is considered public because it can be accessed an dchanged outside of bird's definition.

```
bird.name = "Duffy";
```
Therefore, any part of your code can easily change the name of bird to any value. Think about things like passwords and bank accounts being easily changeable by any part of your codebase. That could cause a lot of issues.

The simplest way to make properties private is by creating a variable within the constructor function. This changes the scope of that variable to be within the constructor function versus available globally. This way, the property can only be accessed and changed by methods also within the constructor function.

```
function Bird() {
    let hatchedEgg = 10;    // private property

    this.getHatchedEggCount = function() {  // publicaly available method that a bird object can use
        return hatchedEgg;
    };
}
let ducky = newBird();
ducky.getHatchedEggCount(); // returns 10
```
Here getHatchedEggCount is a privileged method, because it has access to the provate variable hatchedEgg. This is possible because hatchedEgg is declared in the same context as getHatchedEggCount. In JavaScript, a function always has access to the context in which it was created. This is called closure.

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
Note that the function has no name and is not stored in a variable. The two praentheses() at the end of the the function expression cause it to be immediately executed or invoked. This pattern is known as an **immediately invoked function expression** or **IIFE**.

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

An immediately invoked function expression (IIFE) is often used togroup related functionality into a single object or module. For example, an earlier challenge defined two mixins:

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

<div id="function-programmin"/>

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
25. [Appedix Notes](#25a)

<div id="1a"/>

### Introduction to the Functional Programming Challenges

Functional programming is an approach to software development based around the evaluation of functions. Like mathematics, functions in programming map input to output to produce a result. You can combine basic functions in many ways to build more and more complex programs.

Functional prigramming follows a few core principles:

* Functions are independent from the state of the program of global variables. They only depend on the arguments passed into them to make a calculation.
* Functions try to limit any changes to the state of the program and avoid changes to the global objects holding data.
* Functons have minimal side effects in the program.

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

In English (and many other languages), the imperative tense is used togive commands. Similarly, an imperative style in programming is one that gives the computer a set of statements to perform a task.

Often the statements change the state of the program, like updating global variables. A classic example of writing a for loop that gives exact directions to iterate over the indices of an array.

In contrast, functional programming is a form of declarative programming. You tell the computer what you want done by calling a method or function.

JavaScript offers many predefined methods that handle common tasks so you don't need to write out how the computer should perform them. For example, instead of using the for loop mentioned above, you could call the map method which handles the details of iterating over an array. This helps to avoid semantic errors, like the "Off By One Errors" that were covered in the Debugging section.

Consider the scenario: you are browsing the web in your browser. and want to track the tabs you have opened. The titles of each open site in each Window object is held in an array. After working in the browser (opening new tabs, merging windows, and closing tabs), you want to print the tabs that are still open. Closed tabs are removed from the array and new tabs (for simplicity) get added to the end of it.

The code editor shows an implementation of this functionality with functions for tapOpen(), tabClose(), and join().
The array tabs is part of the Window object that stores the name of the open pages.

Instructions

Run the code in the editor. It's using a method that has side effects in the program, causing incorrect output. The final list of open tabs should be ['FB', 'Gitter', 'Reddit', 'Twitter', 'Medium', 'new tab', 'Netflix', 'YouTube', 'Vine', 'GMail', 'Work mail', 'Docs', 'freeCodeCamp', 'new tab'] but the output will be slighty different. 

Work through the code and see if you can figure out the problem, then advance to the next challenge to learn more

```
// tabs is an array if titles of each site open within the window
var Window = function(tabs) {
    this.tabs =tabs;    // we keep a record of the array inside theobject
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
Fill in the code for the function incrementer so it returns the value of the gloabl variable fixedValue increased by one.

```
// the global variable
var fixedValue = 4;

function incrementer () {
  // Add your code below this line
  
  
  // Add your code above this line
}

var newValue = incrementer(); // Should equal 5
console.log(fixedValue); // Should print 4
```

<div id="6a"/>

### Pass Arguments to Avoid External Dependence in a Function

The last challenge was a step closer to functional programming principles, but there is still something missing.

We didn't alter the global variable value, but the function incrementer would not work without the global variable fixedValue being there.

Another principle of functional programming is to always declare your dependencies explicitly. This means if a function depends on a variable or object being present, then pass that variable or object directly into the function as an argument.

There are several good consequences from this principle. The function is easier to test, you know exactly what input it takes, and it won't depend on anything else in your program.

This can give you more confidence when you alter, remove, or add new code. You would know what you can or cannot change and you can see where the potential traps are.

Finally, the function would always produce the same output for the same set of inputs, no matter what part of the code executes it.

Let's update the incrementer function to clearly declare its dependencies.

Write the incrementer function so it takes an argument, and then increases the value by one.

```
// the global variable
var fixedValue = 4;

// Add your code below this line
function incrementer (fixedValue) {
  return fixedValue + 1;
  
  // Add your code above this line
}

var newValue = incrementer(fixedValue); // Should equal 5
console.log(fixedValue); // Should print 4
```

<div id="7a"/>

### Refactor Global Variables Out of Functions

So, far we have seen two distinct principles for functional programming.

1) Don't alter a variable or object - create new variables and objects and return them if need be from a function

2) Declare function arguments - any computation inside a function depends only on the arguments, and not on any gloabal object or variable.

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

So far we have learned to use pure functions to avoid side effects in a program. Also, we have seen the value in having a function only depend on its inpur arguments.

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

Filter doesn't alter the original array, just like map. It takes a callback function that applies logic inside the callback on each elementof the array. If an element returns true based on the criteria in the callback function. then it is included in the new array.
____________________________________________________________________
The variable watchList holds an array of objects with information on several movies. Use a combination of filter and map to return a new array of objects with only title and rating keys, but where imdbRating is greater than or equal to 8.0. Note that the rating values are saved as strings in the object and you may want to convert them into numbers to perform mathematical operations on them.


<div id="11a"/>

### Implement the filter Method on a Prototype

It would teach us a lot about the filter methid if we try to implement a version of it that behaves exactly like Array.prototype.filter(). It can use either a for loop or Array.prototype.forEach().

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

The slice method returns a copy of certain elements of an array. It can take twwo arguments, the first gives the index of where to begin the slice, the second is the index for where to end the slice (and it's non-inclusive). If the arguments are not provided, the default is to start at the beginning of the array through the end, which is an easy way to make a copy of the entire array. The slice method does not mutate the original array, but returns anew one.

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

A common pattern while working with arrays is when you want to remove items and keep the rest of the array. JavaScript offers the splice method for this, which takes arguments for the index of where to start removing items, then the number of items to remove. If the second argument is not provided, the default is to remove otems through the end. However, the splice method mutates the original array it is called on. 
Here's an example:

```
var cities = ["Chicago", "Dehli", "Islamabad", "London", "Berlin"];
cities.splice(3, 1);  // Returns "London and deletes it from the cities array
// cities is now ["Chicago", "Delhi", "Islamabad", "Berlin"]
```

As we saw in the last challenge, the slice method does not mutate the original array, but returns a new one which can be saved into a variable. Recall that the slice method takes two arguments for the indices to begin and end the slice (the end is non-inclusive), and returns those items in a new array. Using the slice method instead of splice helps to avoid any array-mutaing side effects.
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

The last challenge introduced the concat method as a way to combine arrays into a new one without mutatuing the original arrays. Compare concat to the push method. Push adds an item to the end of the same array it is called on, which mutates that array. Here's an example:

```
var arr = [1, 2, 3];
arr.push([4, 5, 6]);
// arr is changed to [1, 2, 3, [4, 5, 6]]
// Not the functional programming way
```

Concat offers a way to add new items to the end of an array without any mutatuing side effects.
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

This is not the case with the filter and map methods since they do not allow interaction between two different elements of the array. For example, if you want to compare elements of the array, or add them together, filter or map culd not process that . 

The reduce method allows for more general forms of array processing, and it's possible to show that both filter and map can be derived as a special application of reduce.

However, bofore we get there, let's practice using reduce first.
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

Note: It's encouraging to provide a callback function to specify hoew to sort the array items. JavaScript's default sorting method is by string Unicode point value, which may return unexpected results. 
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
Since strings are immutable, the split method maked it easier to work with them.
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

The join method is used to jooin the elements of an array together to create a string. It takes an argument for the delimiter that is used to seperate the array elements in the string.

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

The alst several challenges covered a number of useful array methods that follow functional programming principles. We've also learned about reduce, which is a powerful method used to reduce problems to simpler forms. From computing averages to sorting, any array operationcan be achieved by applying it. Recall that map and filter are special cases of reduce.

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

The some method works with arrays to check if any element passes a particular test. It retruns a Boolean value -true if any of the values meet the criteria, false if not.

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

## Appedix Notes

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
@eaxh $color in blue, red, green {
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
