---
layout: post
title:      "Testing with Jest"
date:       2020-05-02 17:40:16 +0000
permalink:  testing_with_jest
---


One of the things that was covered briefly in my coding camp was using testing.  It explained the basics of how to do it with the backend language, but didn't do a whole lot for the front end.  As I am drawn more towards the front end, and have even picked up Node so I can program backend in JavaScript as well, I felt it was necessary for me to start picking up testing methods using JavaScript.

Several different platforms for this are available, but the one most recommended with React was Jest, so that is where I chose to begin.  I also wanted to start simple with unit testing and work my way up through integration testing and ui testing.  I went to the Jest documentation and they laid out the process very simply.

First start by installing jest to your project:

```
npm install --save-dev jest
```

The save-dev puts the testing framework in the development mode only. 

The next step is to put the script in place.  In the package.json file, there is a scripts object.  Here you want to add "test": "jest"  like so:

```
  "scripts": {
    "test": "jest"
  },
	```
	
	When I installed jest in an app I had already started building, with scripts I had already added, I had to add this manually.  However, when I did it in an empty app, scripts and test were already there that printed out a line about not having specified testing.
	
Next we need to create a function to test.  Since unit testing is testing function by function, I decided to do multiple functions and have multiple tests.  The documentation gives the example of a sum, so I went with the four basic math functions.

```
math.js

math = {
    "sum": (a, b) => {
        return a + b;
    },
    "difference": (a,b) => {
        return a - b;
    },
    "product": (a, b) => {
        return a * b;
    },
    "quotient": (a,b) => {
        return a / b;
    }
}

module.exports = math

```

after this, I created my test file.

```
math = require("./math")


test('adds two numbers to get sum:', ()=>{
    expect(math.sum(1,2)).toBe(3);
})

test('subtracts two numbers', ()=>{
    expect(math.difference(3,2)).toBe(1);
})

test('multiplies two numbers', ()=> {
    expect(math.product(2,3)).toBe(6);
})

test('divides two numbers', ()=> {
    expect(math.quotient(6,2)).toBe(3);
})
```

The top line imports the math object that I created.  Each test line is a test for each function.  It takes in a string that describes the test and a callback function that runs the test.  It is important that the callback test returns a boolean.  You could write your own functions testing the code, but the given expect and toBe make it simple.

After this, you simply run the test by:

```
npm run test
```

the results should look something like this:

```
$ npm run test

> testingplayground@1.0.0 test C:\Users\teach\OneDrive\Desktop\testingplayground
> jest

 PASS  ./math.test.js
  √ adds two numbers to get sum: (2ms)
  √ subtracts two numbers
  √ multiplies two numbers
  √ divides two numbers (1ms)

Test Suites: 1 passed, 1 total
Tests:       4 passed, 4 total
Snapshots:   0 total
Time:        1.885s
Ran all test suites.

```
