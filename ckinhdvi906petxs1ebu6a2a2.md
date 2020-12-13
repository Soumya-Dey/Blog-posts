## Make Arrays your best friend with these methods

I know many people have already written a lot about arrays, but most of them only contain the most used and basic methods.

But there are lots of not so popular methods that you can use to manipulate, iterate, and do many things with your arrays. So we are going to talk about those methods in this post using JavaScript.

<hr>

## Arrays
JavaScript array is a non-primitive data type that can store multiple values in it which can be of the same data type or different data type. Also, the length of a JavaScript array is not fixed.

## Array methods

We all know about `push()`, `pop()`, `indexOf()` methods.
`arr.push('x')` adds `x` at the end of the array `arr` and `arr.pop()` removes the last item from `arr`.
`arr.indexOf('x')` finds the index of `x` in `arr`.

**So let's talk about the unpopular but equally important guys here.**

### Manipulate arrays

- **unshift()**

The `unshift()` method _adds the new element at the beginning of the array_ and returns the new length of the array.

Example
```js
const array = ["world"];
array.unshift("hello"); // 2

console.log(array); // ["hello", "world"]
```

- **shift()**

The `shift()` method _removes the first element from the array and returns the removed element_. It also changes the length of the array.

Example
```js
const array = ["hello", "world"];
array.shift(); // "hello"

console.log(array); // ["world"]
```

- **slice()**

The `slice()` method returns a _shallow copy of a portion of an array into a new array object selected from start to end_, excluding the item at the end index. The original array is not modified

Example
```js
const array = ["js", "py", "java", "c++", "c#"];

array.slice(3); // [ 'c++', 'c#' ]

array.slice(0, 2); // [ 'js', 'py' ]

console.log(array); // ["js", "py", "java", "c++", "c#"]
```

- **splice()**

The `splice()` method changes the contents of an array by _removing or replacing existing elements and/or adding new elements in place_.

Example
```js
const array = ["js", "py", "java", "c++", "c#"];

array.splice(0, 2); // delets 2 items starting from index 0
console.log(array); // ["java", "c++", "c#"]

array.splice(0, 1, 'kotlin');
// delets 1 item starting from index 0,
// and puts 'kotlin' in that place
console.log(array); // ["kotlin", "c++", "c#"]
```

- **join()**

The `join()` method _creates and returns a new string by concatenating all of the elements in an array_ separated by commas or a specified separator string.

Example
```js
const array1 = ["1", "2", "3"];
array1.join(); // "1,2,3"

const array2 = ["I", "love", "programming"];
array2.join("-"); // "I-love-programming"
```

- **concat()**

The `concat()` method is used to _merge two or more arrays_. This method does not change the existing arrays but instead returns a new array.

Example
```js
const array1 = ['a', 'b', 'c'];
const array2 = ['d', 'e', 'f'];
const array3 = array1.concat(array2);

console.log(array3); // ["a", "b", "c", "d", "e", "f"]
```

### Iterate over arrays 

- **every()**

The `every()` method _tests whether all elements in the array pass the test implemented by the provided function_. It returns a Boolean value.

Example
```js
const array = [10, 2, 1, 13, 17, 19, 6, 9];

array.every(item => item > 4) // false
array.every(item => item < 20) // true
```

- **some()**

The `some()` method tests whether at least one element in the array passes the test implemented by the provided function. It returns a Boolean value.

Example
```js
const array = [1, 2, 3, 4, 5];

// checks whether an element is even
array.some(item => item % 2 === 0); // true
```

- **map()**

The `map()` method creates a new array populated with the results of calling a provided function on every element in the calling array.

Example
```js
const array = [1, 2, 3, 4, 5];

const doubleOfArray = array.map(item => item * 2);

console.log(doubleOfArray); // [2, 4, 6, 8, 10]
```

- **filter()**

The `filter()` method creates a new array with all elements that pass the test implemented by the provided function.

Example
```js
const array = [1, 2, 3, 4, 5];

// only the element that are even
const evenArray = array.filter(item => item % 2 === 0);

console.log(evenArray); // [2, 4]
```

### Reduction methods

- **reduce()**

The `reduce()` method _executes a reducer function defined by you on each element of the array_, resulting in a single output value.

Example
```js
const array = [1, 2, 3, 4, 5];

// ((((1-2)-3)-4)-5) = -13
const result = array.reduce((accumulator, current) => accumulator - current);

console.log(result); // -13
```

- **reduceRight()**

The `reduceRight()` method _applies a function against an accumulator and each value of the array (from right-to-left) to reduce it to a single value_.

Example
```js
const array = [1, 2, 3, 4, 5];

// ((((5-4)-3)-2)-1) = -5
const result = array.reduceRight((accumulator, current) => accumulator - current);

console.log(result); // -5
```

### Sorting arrays

- **sort()**

The `sort()` method _sorts the elements of an array in place_ and returns the sorted array. The default sort order is ascending.

Example
```js
const months = ['March', 'Jan', 'Feb', 'Dec'];
const nums = [4, 6, 2, 5, 1, 7, 3]

months.sort();
nums.sort();

console.log(months); // ["Dec", "Feb", "Jan", "March"]
console.log(nums); // [1, 2, 3, 4, 5, 6, 7]
```

- **reverse()**

The `reverse()` method _reverses an array in place_ and returns the sorted array. Don't confuse it with sorting in descending order.

Example
```js
const nums = [4, 6, 2, 5, 1, 7, 3]

nums.reverse();

console.log(nums); // [3, 7, 1, 5, 2, 6, 4]
```

<hr>

That's it. You have made a new best friend now.

Thanks for reading.
If you want to get a deeper knowledge of Arrays in JavaScript then make sure to read the MDN docs of Array here 👉 [Array - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)

### Comment here if you have any questions about these awesome array methods.

If you like my blogs [Follow me on Dev.to](https://dev.to/soumyadey)

[My Github](https://github.com/Soumya-Dey)