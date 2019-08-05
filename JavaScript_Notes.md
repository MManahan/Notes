# Java Script Notes

#### In order to run a javascript file in html code, input script for .js file

```
<script type="text/javascript" src="app.js"></script>
```
```
console.log()
```
#### This displays or "prints" output into console

#### JS has strings and numbers as data types. In order to turn a string into a integer, you use 
```
parstInt(string)
```
#### Same way we print out the f' string in python, we use the dollar sign and the curly brackets in the string to call the value

```
${variable}
```
#### JS uses triple === to check condition. The third "=" checks to see if it is the same datatype. 

### If Statements
#### have the following format
```
if (y < 5) {
  console.log("x is less than 10 and y is less than 5");
}
else if (y === 5) {
  console.log("x is less than 10 and y is equal to 5");
}
else {
  console.log("x is less than 10 and y is greater than 5");
}
```
### Arrays
#### Similar to Python lists. 
```
var lettersArray = ["a", "b", "c", "d"];
```
#### Index arrays
```
var firstLetter = lettersArray[0];
var secondLetter = lettersArray[1];
```
#### Append arrays
```
lettersArray.push("e");
lettersArray.push("f");
```
#### Slice arrays
```
var slicedArray1 = lettersArray.slice(1);
// Return the first three items of an array
var slicedArray2 = lettersArray.slice(0, 3);
// Return the second and third items of an array
var slicedArray3 = lettersArray.slice(1, 3);
```
#### Join items of array into a single strimng
```
var joinedArray = lettersArray.join(", ");
```
#### .split, splits string into individual elements given delimiter. In this case, the delimiter was a space
```
var soundArray = soundOfMusic.split(" ");
```
## For Loops
#### Long structure of for loop:
```
for (var i = 0; i < 10; i++) {
  console.log("Iteration #", i);
}
```
#### Long way of Looping through array:
```
var students = ["Johnny", "Tyler", "Bodhi", "Pappas"];

for (var j = 0; j < students.length; j++) {
  console.log(students[j]);
}
```
## Functions
```
// Simple log statement
function printHello() {
  console.log("Hello there!");
}

// Takes two numbers and adds them
function addition(a, b) {
  return a + b;
}

// This function accepts a parameter and iterates through an array
function listLoop(userList) {
  for (var i = 0; i < userList.length; i++) {
    console.log(userList[i]);
  }
}

var friends = ["Sarah", "Greg", "Cindy", "Jeff"];
listLoop(friends);

// Functions can call other functions
function doubleAddition(c, d) {
  var total = addition(c, d) * 2;

  return total;
}
```
## For each
#### You can use .forEach() to iterate through arrays
```
// Loop through each student name and call the printName function
for (var i = 0; i < students.length; i++) {
  printName(students[i]);
}

// `forEach` automatically iterates (loops) through each item and
// calls the supplied function for that item.
// This is equivalent to the for loop above.
students.forEach(printName);

// You can also define an anonymous function inline
students.forEach(function(name) {
  console.log(name);
});
```
## .Map 
#### creates an array after iterating through an array with the result of the function being called. The first argument is the current item, the second argument returns the index of the current element. 
```
var mapArrayWithIndex = theStagesOfJS.map(function(item, index) {
  return `Stage ${index}: ${item}`;
});

console.log(mapArrayWithIndex);
```
#### The code above returns mapArrayWithIndex, which is just an array from the stagesofJS but also shows the index.
### **Whats the difference between .forEach and .map?**
##### Well, the forEach() method doesn’t actually return anything (undefined). It simply calls a provided function on each element in your array. This callback is allowed to mutate the calling array.
##### Meanwhile, the map() method will also call a provided function on every element in the array. The difference is that map() utilizes return values and actually returns a new Array of the same size. 

## Arrow Functions
```
// An Arrow function is a new concise syntax for function
// Arrow functions allow us to drop the `function` keyword and just show the parameters.
// Note: The fat arrow `=>` that was added to indicate an arrow function.
var mapArrow1 = theStagesOfJS.map((item) => {
  return item;
});
```
## ** .Filter() **
#### You can think of filter() as a for loop, that is specifically for filtering in/out certain values from an array.

## D3.js
#### In my own words, D3 is a JS library that allows the transformation/manipulation of html code for data visualization using the code standards of HTML and CSS. The way of accessing data and inputting data into the html elements is similar to beautiful soup. 

### to grab class attritbutes, you need the dot. for example 
```
var text1 = d3.select(".text1").text()
```
#### Assumming the class name is "text1" the code above gets the element with the class "text1" and gets the text of that element. 
#### You can also modify the text of the element by passing in the string inside .text(). 
```
d3.select(".text1").text("Hey, I changed this!");
```
#### You can select an element's child with ">". For example
```
var myLinkAnchor = d3.select(".my-link>a");
```
#### In the above code, .my-link is the class of the parent element to the anchor element "a" which is the child. Since a, or anchor tags usually contain a link as an attribute, you can grab the link by :
```
myLinkAnchor.attr("href")
```
#### This returns the link in the anchor tag. 

#### How to change attribute
```
myLinkAnchor.attr("href", "https://python.org");
```
