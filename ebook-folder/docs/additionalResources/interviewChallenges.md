# Interview Challenges

## Why Train for Interviews?

Interviewing for development jobs is tough! To prepare you for the challenges ahead we will practice whiteboarding in front of the class every day. Think of it as a warm-up for the project that awaits. The whiteboarding challenges should be taken seriously and practiced even outside of class. Help yourself by following these steps to attack the problem, work through the problem and collaborate with your interviewer (instructor):

## How to Solve Your Challenge

**Restate**, **rewrite**, and **clarify** the question. Write the **expected return** given the input. Make a code plan and speak aloud **with** your interviewers/team. **Test** and come up with edge cases. **Revise** if you can for efficiency.

**Restate, Rewrite, Clarify, Return, Plan, Collaborate, Code, Test, Revise**

- [ ] Restate the question aloud.
- [ ] Write the question out at the top of the whiteboard.
- [ ] Ask any clarifying questions you need.
- [ ] Invoke the function and write out the expected output given the sample input. If none is given, make it up.
Write out a code plan to the side of the whiteboard.
Speak aloud every thought you have. THIS IS THE MOST IMPORTANT PART!
- [ ] Build the structure of your function(s).
- [ ] Slowly work through your code plan, building the steps you need.
- [ ] Don't be afraid to mess up and say it aloud.
- [ ] It's not about finding the solution. It's about collaborating and working toward a solution!
- [ ] After you finish, take a screenshot( ++cmd+shift+3++ || ++alt++ + PrtScn) and transfer it to a Repl.it when you get home.

<!-- ```javascript
  // optional code example
``` -->

## The Prompts

### Class 1

- [ ] **Prompt 1: Using HTTP and APIs** - *All together at the same time. We'll hear thoughts and discussion afterward.*

    - [ ] Write out the URI to get an individual character from the Star Wars API. Highlight the pieces of the URI and explain what they mean.
    - [ ] Explain what is included in an HTTP request message. Write it out and explain the parts.
    - [ ] Explain what is included in an HTTP response message. Write it out and explain the parts.
    - [ ] Diagram what happens when a client makes a GET request. What is included in the request? - [ ] What is included in the response?
    - [ ] Diagram a POST request to create a resource. What is included in the request? What is included in the response?

### Class 2

- [ ] **Prompt 1: sumOneForOne** - *There are two arrays with individual values. Write a JavaScript program to compute the sum of each individual index value from the given arrays.*

```javascript
    let array1 = [1, 0, 2, 3, 4]; 
    let array2 = [3, 5, 6, 7, 8, 13];

    const sumOneForOne = () => { /*your code here*/}

    sumOneForOne(array1, array2) // => [4, 5, 8, 10, 12, 13]
```

- [ ] **Prompt 2: RESTful Design** - *Design a REST API for a photo album site.*

    * [ ] *What resources would the API support?*
    * [ ] *What operations can be done on those resources, and what HTTP verb would be used for each?*
    * [ ] *What would the body of a request and response look like for each operation?*
    * [ ] *For this first whiteboarding challenge, the instructor will lead the discovery.*

    > The Instructor will lead this discussion with input from the class.

### Class 3

- [ ] **Prompt 1: Title** - *Your customer has sa list of volume, which you have neatly stored into an array. One of the properties of each volume is a protection policy. The customer wants their users to be able to apply a protection policy to new volumes globally, if all of the existing volumes have the same policy. You need to write a function that returns a boolean. `true`, meaning all the policies in the array are the same, or `false`, meaning at least one policy in the array is different from another.*

*The caveat here is, new volumes are also in this array, and their policy is denoted as a special string `'--:--'`. This means there is no policy on the volume and thus, the volume is new. If all the policies in the array are the same, we can apply that policy globally TO the new volumes, else, we cannot, and will have to go new-volume by new-volume, applying policies individually.*

*Policies are denoted with characters 'A' 'B' 'C' or 'D'. New volume policies are denoted with the special string `'--:--'`.*

```console
    INPUT: [ {policy: 'A'}, {policy: 'A'}, {policy: '--:--'}, {policy: '--:--'}, {policy: 'A'}, {policy: 'A'},]

    OUTPUT: true, set global policy

    INPUT: [ {policy: 'A'}, {policy: 'B'}, {policy: '--:--'}, {policy: '--:--'}, {policy: 'A'}, {policy: 'C'},]

    OUTPUT: false, prevent global policy
```

*With this data, build a function that determines if setting a global policy is possible or not.*

<!-- - [ ] **Prompt 2: Title** - *description* -->

### Class 4

- [ ] **Prompt 1: getNArray** - *Write a JavaScript function to get the first element of an array. BUT passing a parameter 'n' will return the first 'n' elements of the array.*

```javascript
    getNArray([7, 9, 0, -2]); // --> 7
    getNArray([],3); // --> []
    getNArray([7, 9, 0, -2],3); // --> [7, 9, 0]
    getNArray([7, 9, 0, -2],6); // --> [7, 9, 0, -2]
    getNArray([7, 9, 0, -2],-3); // --> []
```
<!-- - [ ] **Prompt 2: Title** - *description* -->

### Class 5

- [ ] **Prompt 1: ArrayClone** - *Write a JavaScript function to clone an array.*

```javascript
    console.log(cloneArray([1, 2, 4, 0]));  // => [1, 2, 4, 0]
    console.log(cloneArray([1, 2, [4, 0]])); // => [1, 2, [4, 0]]
```

### Class 6

- [ ] **Prompt 1: Binary Search** - *Write a JavaScript program to perform a binary search.*

    > Note: A binary search or half-interval search algorithm finds the position of a specified input value within an array sorted by key value.*

    ```javascript
        // Sample array :
        const items = [1, 2, 3, 4, 5, 7, 8, 9];
        // Expected Output :
        console.log(binary_Search(items, 1)); // --> 0
        console.log(binary_Search(items, 5)); // --> 4
    ```
<!-- - [ ] **Prompt 2: Title** - *description* -->

### Class 7

- [ ] **Prompt 1: deDup** - *Given a sorted array of numbers, remove the duplicates in-place such that each unique element appears only once and return the new length.*

```javascript
    function deDup(array){
        // ...your code here...
    }

    let test1 = [1,1,2];
    console.log(deDup(test1)) // 2
    console.log(test1) //[1,2,null]

    let test2 = [1,2,3,3,3,4,4,4,5];
    console.log(deDup(test2)) // 5
    console.log(test2); // [1,2,3,4,5,null,null,null,null]

    let test3 = [1,1,1,1,2,3,3,3,4,4,4,5]; 
    console.log(deDup(test3))  // 5
    console.log(test3) // [1,2,3,4,5]

    let test4 =[1,2,3,4,5,6,7,8,9];
    console.log(deDup(test4)) // 9
    console.log(test4) //[1,2,3,4,5,6,7,8,9]
```

### Class 8

- [ ] **Prompt 1: Technical Question** - *What are the security threats full stack developers must be aware of?*
<!-- - [ ] **Prompt 2: Title** - *description* -->

### Class 9

- [ ] **Prompt 2: Two Digits Only** - *How would you format a string to always show two significant digits after the decimal? For Example: 1 => 1.00 or 4.5 => 4.50, 7.888888=> 7.88.*

    > NOTE: Can’t use `.toFixed`

### Class 10

- [ ] **None today.**
<!-- - [ ] **Prompt 2: Title** - *description* -->

### Class 11

- [ ] **Prompt 1: firstNoRepeat** - *Given a string, return the index of the first non-repeating character in the string. If none exist, return -1.*

```javascript
firstNoRepeat("seat") // 0

firstNoRepeat("lollipop") // 4

firstNoRepeat("poop") // -1
```

### Class 12

- [ ] **Prompt 1: Best Profit** - *Take an array of prices where each index in the array represents a time, i.e. every minute or every hour. Build an algorithm to find out what your best profit could have been if you bought at the lowest price and sold at the highest price, **after you bought**. You must buy before you sell.*

```javascript
 const myArr = [75, 39, 44, 1, 8, 10, 1, 11, 2, 3, 4, 5]

findBestSellAndBuy(myArr) // -->  { maxProfit: 10, bestBuyIndex: 3, buyPrice: 1, bestSellAt: 7, sellPrice: 11 }
```

### Class 13

- [ ] **Prompt 1: Recursive Permutation** - *Write a recursive function for generating all permutations of an input string. Return them as a set.*

    > * Don't worry about time or space complexity—if we wanted efficiency we'd write an iterative version.
    > * To start, assume every character in the input string is unique.
    > * Your function can have loops in it—it just also needs to be recursive.
    > * What's a permutation?
    > * What's recursion?
<!-- - [ ] **Prompt 2: Title** - *description* -->

### Class 14

- [ ] **Prompt 1: Figure it Out** - *Given an array of numbers, return an array of paired subset numbers in descending order based on their sums.*
<!-- - [ ] **Prompt 2: Title** - *description* -->

### Class 15

- [ ] **Prompt 1: Title** - *The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)*

```markdown
P   A   H   N
A P L S I I G
Y   I   R
```

```javascript
const convertZigZag = (string,numRows) => { 
    // your code here
}

// Example 1:
convertZigZag("PAYPALISHIRING", 3) // --> Output: "PAHNAPLSIIGYIR"

// Example 2:
convertZigZag("PAYPALISHIRING", 4) // --> Output: "PINALSIGYAHRPI"

// Explanation:

// P     I     N
// A   L S   I G
// Y A   H R
// P     I
```

### Class 16

- [ ] **Prompt 1: Automatic Delivery Network** - *Your company delivers breakfast via autonomous quadcopter drones, and something mysterious has happened.*

- [ ] *Each breakfast delivery is assigned a unique ID, a positive integer. When one of the company's 100 drones takes off with a delivery, the delivery's ID is added to an array, deliveryIdConfirmations. When the drone comes back and lands, the ID is again added to the same array.*
- [ ] *After breakfast this morning there were only 99 drones on the tarmac. One of the drones never made it back from a delivery. We suspect a secret agent from Amazon placed an order and stole one of our patented drones. To track them down, we need to find their delivery ID.*
- [ ] *Given the array of IDs, which contains many duplicate integers and one unique integer, find the unique integer.*
- [ ] *The IDs are not guaranteed to be sorted or sequential. Orders aren't always fulfilled in the order they were received, and some deliveries get cancelled before takeoff.*


<!-- 2. [Class 2](01Week/02DayClass.md) -
    * **Prompt 1**: *Reverse an array of strings such at input= "red","black","blue","yellow" output = "yellow","blue","black","red"*
    * **Prompt 2**: *How do you find the largest and smallest number in an unsorted integer array?*
3. [Class 3](02Week/01DayClass.md) -
    * **Prompt 1**: *How do you find all pairs of an integer array whose sum is equal to a given number?*
        i.e. `sumPairs(arr, 16)` => `[8, 8], [14, 2], [10, 16], [1, 15], [32, -16]`
    * **Prompt 2**: *How do you find the missing number in a given integer array of 1 to 100?*
4. [Class 4](02Week/02DayClass.md) -
    * **Prompt 1**: *How do you check if two strings are anagrams of each other? Build a program that does just that.*
5. [Class 5](03Week/01DayClass.md) -
    * **Prompt 1**: *How can a given string be reversed using recursion? Build a program to do that.*
6. [Class 6](03Week/02DayClass.md) -
    * **Prompt 1**: *How is a binary search tree implemented?*
7. [Class 7](04Week/01DayClass.md) -
    * **Prompt 1**: *How do you count a number of leaf nodes in a given binary tree?*
8. [Class 8](04Week/02DayClass.md) -
    * **Prompt 1**: *How do you perform a binary search in a given array?*
9. [Class 9](05Week/01DayClass.md) -
    * **Prompt 1**: *How do you implement an insertion sort algorithm?*
10. [Class 10](05Week/02DayClass.md) -
    * **Prompt 1**: *How do you implement a bucket sort algorithm?*
11. [Class 11](06Week/01DayClass.md) -
    * **Prompt 1**: *How is a radix sort algorithm implemented? Build one.*
12. [Class 12](06Week/02DayClass.md) -
    * **Prompt 1**: *How do you swap two numbers without using the third variable?*
13. [Class 13](07Week/01DayClass.md) -
    * **Prompt 1**: *Define a function that returns n lines of [Pascal’s Triangle](https://en.wikipedia.org/wiki/Pascal%27s_triangle).*
14. [Class 14](07Week/02DayClass.md) -
    * **Prompt 1**: *Use recursion to log a fibonacci sequence of n length.*
15. [Class 15](08Week/01DayClass.md) -
    * **Prompt 1**: *Define a function that takes an array of strings, and returns the most commonly occurring string that array*
16. [Class 16](08Week/02DayClass.md) -
    * **Prompt 1**: *You have 1000 bottles of soda, and exactly one is poisoned. You have 10 test strips which can be used to detect poison. A single drop of poison will turn the test strip positive permanently. You can put any number of drops on a test strip at once and you can reuse a test strip as many times as you'd like (as long as the results are negative.) However, you can only run tests once per day and it takes seven days to return a result. How would you figure out the poisoned bottle in as few days as possible?*

        *Write code to simulate your approach.* -->