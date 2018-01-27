---
layout: post
title: Javascript Basics
tags: [javascript]
categories: notes
--- 
- statements end in **;**
- var myName = "An"/true/6; 
- var a = new Array(size); 
- document.write(stringToPrint);   
- function foo(who) {
    console.log("blah" + who);
}
- if (a>10) {alert(a);}
- concat Strings by '+'
- **strict equal** 3 ==='3' and 3 !== '7'
- logical operators &&
- strings are **immutable** once created but can be reassigned
- var myArray = [ elements need not be of same type]
    - array.push() to append
    - array.unshift() to prepend
    - array.pop() to get item popped from the end
    - array.shift() to get item popped from the front
- switch 
``` Javascript
function caseInSwitch(val) {
  var answer = "";
  // Only change code below this line
  switch (val) {
    case 1:
      return "alpha";
      break;
    case 2:
      return "beta";
      break;
    case 3:
      return "gamma";
      break;
    case 4:
      return "delta";
      break;
  }
  answer = val;
  return answer;  
}
```
- **Object** 
    - the data in object are called **properties**.
    ```Javascript
    var cat = {
  "name": "Whiskers",
  "legs": 4,
  "tails": 1,
  "enemies": ["Water", "Dogs"]
    };
    a = cat.name;
    b = cat["legs"];
    delete cat.tails;

    cat.hasOwnProperty(propName)
    ```
- JavaScript Object Notation or **JSON** is a related data interchange format used to store data, a list of Objects.
- Math.random() returns 0(inclusive) to 1(exclusive)
  - Math.floor() rounds down 
- /word/gi 
  - g stands for global which allows this RegEx to find all matches rather than stop at the first match
  - \d num
  - \s whitespace
  - \S Non-whitespace
- We are also able to create objects using constructor functions.
  - A constructor function is given a capitalized name to make it clear that it is a constructor.
  ```Javascript
  var Car = function() {
  this.wheels = 4;
  this.engines = 1;
  this.seats = 5;
  var privateVar = 2;
  };
  var myCar = new Car();
  ```
These are all methods:
- map()
```Javascript
var oldArray = [1, 2, 3];
var timesFour = oldArray.map(function(val){
  return val * 4;
});
console.log(timesFour); // returns [4, 8, 12]
console.log(oldArray);  // returns [1, 2, 3] DOES NOT MODIFY ORIGINAL ARRAY
```
- reduce() is like accumulator
```Javascript
var singleVal = array.reduce(function(previousVal, currentVal) {
  return previousVal - currentVal;
}, 0);
```
- filter
- split

- 
```Javascript
$(document).ready(function() {
  $("button").addClass("animated bounce");
  $(".generate-quote").css('color', 'blue');
  $("#target1").prop("disabled", true);
  $("h3").text("<em>jQuery Playground</em>");
  $("h3").html("<em>jQuery Playground</em>");
  $("#target4").remove();
  $("#target2").appendTo("#right-well");
  $("#target5").clone().appendT("#left-well");
  $("#target1").parent().cs("background-color", "red");
  $("#right-well").children().css("color","orange");
  $(".target:nth-child(2)").addClass("animated bounce"); 
  });
```