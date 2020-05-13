---
title: Unit Testing Explained
date: "2020-04-01T23:46:37.121Z"
description: What are tests? Why test? How testing is done in JavaScript?
---

### What are tests?

It’s as simple as the name suggests. We expect something to work as expected and we check if it does. We want our program to work as expected, so we test it. You may have seen testing files with the naming convention filename.test.js. It is the file where we specify or assert what our code should do and then test it to verify it does it.

You have two choices when it comes to testing: manual testing and automated testing.

- **Manual Testing:** It is the process of checking your application or code from the user’s perspective. Opening up the browser or program and navigating around in an attempt to test functionality and find bugs.

- **Automated Testing:** It is writing a code that checks to see if other code works. Contrary to manual testing, the specifications remain constant from test to test. The biggest advantage is being able to test many things much faster.

### Why test?

You may think, “Hey, why write a separate program to check another program?” Yeah, we could easily check for issues if our code is only a few lines. But think of a program with more than 1000 lines with asynchronous functions, values jumping from one part of the program to the other, etc.<br>
In this case, even a small mistake in naming a variable or typo could make the program behave unexpectedly. And it would be a nightmare debugging the logic and 1000 lines of code. So this is where we might wanna write tests for our code.

### First Let's Talk about different types of testing

Before we dive into unit testing specifics, I want to do a quick run through of the different types of tests. There is often some confusion around them. Sometimes the line between them is quite thin.

#### Unit tests
Unit tests only test a single part of your implementation. A unit. No dependencies or integrations, no framework specifics. They're like a method that returns a link in a specific language:

#### Integration tests
At some point, your code communicates with a database, file system or another third party. It could even be another module in your app. That piece of implementation should be tested by integration tests. They typically have a more complicated setup that involves preparing testing environments, initializing dependencies, and so on.

#### Functional tests
Unit tests and integration tests give you confidence that your app works. Functional tests look at the app from the user's point of view and test that the system works as expected.

![presentation](./presentation.jpg)

In the diagram above, you see that unit tests form the large base of your application's testing suite. Typically, they are small, there are a lot of them, and they are executed automatically.

Now we have a brief overview of testing, but we are here to learn about unit testing.

### Why Should I Bother Writing Unit Tests?

  1. **Less time performing functional tests:**<br>
        Functional tests are expensive. They typically involve opening up the application and performing a series of steps that you (or someone else), must follow in order to validate the expected behavior. These steps may not always be known to the tester, which means they will have to reach out to someone more knowledgeable in the area in order to carry out the test. Also this process must be repeated for every change that you make in the system.<br><br>
        Unit tests, on the other hand, take milliseconds, can be run at the press of a button and do not necessarily require any knowledge of the system at large. Whether or not the test passes or fails is up to the test runner, not the individual.

  2. **Protection against regression:**<br>
        Regression defects are defects that are introduced when a change is made to the application. It is common for testers to not only test their new feature but also features that existed beforehand in order to verify that previously implemented features still function as expected.<br><br>
        With unit testing, it's possible to rerun your entire suite of tests after every build or even after you change a line of code. Giving you confidence that your new code does not break existing functionality.

  3. **Executable documentation:**<br>
        It may not always be obvious what a particular method does or how it behaves given a certain input. You may ask yourself: How does this method behave if I pass it a blank string? Null?<br><br>
        When you have a suite of well-named unit tests, each test should be able to clearly explain the expected output for a given input. In addition, it should be able to verify that it actually works.

  4. **Less coupled code:**<br>
        When code is tightly coupled, it can be difficult to unit test. Without creating unit tests for the code that you're writing, coupling may be less apparent.<br><br>
        Writing tests for your code will naturally decouple your code, because it would be more difficult to test otherwise.

#### Some Characteristics of a good unit test

- **Fast:** It is not uncommon for mature projects to have thousands of unit tests. Unit tests should take very little time to run. Milliseconds.
- **Isolated:** Unit tests are standalone, can be run in isolation, and have no dependencies on any outside factors such as a file system or database.
- **Repeatable:** Running a unit test should be consistent with its results, that is, it always returns the same result if you do not change anything in between runs.
- **Self-Checking:** The test should be able to automatically detect if it passed or failed without any human interaction.
- **Timely:** A unit test should not take a disproportionately long time to write compared to the code being tested. If you find testing the code taking a large amount of time compared to writing the code, consider a design that is more testable.

### By Now, I think I have sold you enough about the importance of Unit Testing. Now let's learn how to write unit tests in Javascript.

There are various frameworks for testing JavaScript code like Mocha, Jest, etc. And in this article, we will be using **Jest** for testing though you can use Mocha or any other libraries you like.

![jest](./jest.png)

[Jest](https://jestjs.io/) is a JavaScript testing framework that enables automatic unit testing, provides code coverage, and lets us easily mock objects. Jest also has an extension for Visual Studio Code available [here](https://marketplace.visualstudio.com/items?itemName=Orta.vscode-jest).

  1. For the setup, we need [NPM](https://www.npmjs.com/) and [Node](https://nodejs.org/en/). So if you haven’t installed it on your system, go on and install. If you have it, then proceed.

  2. Create a folder with any name you like. Am going to create a folder with `mkdir test-jest` and cd into it `cd test-jest`.

  3. Since we will be installing Jest as a package, we need to initialize our folder with NPM with `npm init`.

  4. We can now add Jest with ` npm install --save-dev jest`. We need to add it as a developer dependency and hence we use the flag `--save-dev`.

  5. In your `package.json` file, you might need to change the test script command as jest so we can just run npm test whenever we need to test our code. 

  6. Now, we can create our JavaScript file named `functions.js` to write our code which will be tested using Jest.

  7. Create new folder name `Test` and inside that create a file `functions.test.js`. This is the file in which we'll write test cases. 

  8. In our `functions.js` file, let's keep things simple and basic. Write the following code to test.

```shell
    const functions = {
        sum: (a, b) => {
            return a + b
        },
        subtract: (a, b) => {
            return a - b
        },
        copyArray: (a) => {
            return [... a]
        }
    }
    module.exports = functions
```

  9. Open `functions.test.js` and write the following code.

```shell
    const functions = require('../functions.js')

    test('adds properly', () => {
         expect(functions.sum(1, 5)).toBe(6)
    })

    test('subtracts properly', () => {
         expect(functions.subtract(1, 2)).toBe(-1)
    })
```
  > Note that functions in `module.exports` is not the filename. 
  > Instead, it’s the name of the object we have declared. 
  > And you can write down the functions separately too instead 
  > of using an object. But don’t forget to export each of them.

  10. Now run `npm test` and hurray!🏆 That’s it! We have our tests now. You may see the test pass in the terminal and it’s expected as we have our functions & tests bug-free.

### But we don't understand what’s there in the test. So let us break down the code now.

- In our test file, the first thing we wanna do is to import the module that is needed from our JavaScript file. In our case, we exported the functions object. So let us import that using `const functions = require('../functions.js')`. Now our test file knows the functions inside our object from the `functions.js` file.

- Then we have a function called `test` which has two params. The first one is simply a string that defines what we wanna do or what the test is gonna do. The second param is again a function.

- In the function, we expect something to be something. And in our case, we expect the `add` function to return the sum of whatever the params we pass to it. So `expect(functions.add(1, 5)).toBe(6)` is the test case we have defined for our `add` function.

- Similarly, we expect the results to be something for the `subtract` function too.

That is a raw explanation of what’s written there. But there are several terminologies that Jest has which we need to understand.
```shell
    test
    expect
    matches (toBe, not.toBe, toEqual, etc)
```

#### test
_**‘test’**_ is simply a keyword in Jest. We write tests by using a function provided by Jest called test. It takes in two parameters, a string of what the test is gonna do and another function where we write our actual test. The syntax goes by, `test("", () => {})`

  - The first parameter is simply a definition of what the test is going to do.
  - The second parameter which is a function takes in the actual testing stuff. We use ‘expect’ and ‘matchers’ within this function.

#### expect
_**‘expect’**_ is also a keyword in Jest. As the name suggests, we expect something from our function or the code we have written. The overall syntax goes by, `expect().matcher()`

  - Within the expect function, we provide the inputs for our code from which we are expecting something.
  - `.matcher` is where we use different matchers like _toBe, toEqual, etc._ Consider these as the conditions the result from expect needs to match. It’s more of a kind of `‘==’`.

#### matchers
_**‘matchers’**_ is not a keyword in Jest but is used to call a collection of methods in Jest. There’s a whole lot of matchers in Jest such as,
```shell
    toBe
    toEqual
    toBeDefined
    toBeFalsy, etc.
```
You can find a whole lot of them [here](https://jestjs.io/docs/en/expect).<br>
A typical example would be the one we used in our test file, `expect(functions.add(1, 5)).toBe(6)`. Here, the matcher used is `toBe`. In more simple terms, we are just doing a check like, is _‘1+5 == 6`?_ If so, we get the test passed.<br>

> Note that there are various matchers available in Jest and 
> it’s impossible to mention everything here. So have a look 
> at their [documentation](https://jestjs.io/docs/en/expect). It’s pretty simple and self-explanatory. 
> The only thing you need to know is which matcher to use where.

#### toEqual
Remember we haven’t written a test for the copyArray function? Cause for this test, we will be using a different matcher called _toEqual_. So our test would be,
```shell
    test('copies a new array', () => {
    let arr = [1, 2, 3]
    expect(functions.copyArray(arr)).toEqual([1,2,3])
    })
```
In this example, we used `toEqual` instead of `toBe` because, in our function from the JavaScript file,
```shell
    copyArray: (a) => { return [... a] }
```
we used the spread operator `[... a]`. And this would copy the contents of the array a we passed and returns a new array.<br><br>
So, if we use _toBe_, the compiler throws an error since the elements might be the same but not the location. The new array is created in a different location with the same elements of the array we passed on to the function. Hence we need to use _toEqual_ to check accordingly and exactly.

### Testing Advanced Functionality
By now, we have now learned the low-level basics of Jest. Since our example code is only a few functions, it’s already a unit size. But for large programs, testing each smallest unit of the code is necessary and is what makes unit testing useful before going for production. <br><br>
So how to write tests for some code with complex functionality? There is more advanced stuff like [asynchronous testing](https://jestjs.io/docs/en/asynchronous), [snapshots](https://jestjs.io/docs/en/snapshot-testing), [mocking a service](https://jestjs.io/docs/en/mock-functions), [using jest with selenium](https://github.com/LambdaTest/jest-selenium-webdriver-sample), etc. My main goal with this article was to get you started with the unit testing. For advance topics, we will talk about some other day. <br>

#### Until then, try some testing on your own with maybe some better functions than me :) See ya! 👋





    
