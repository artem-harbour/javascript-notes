# JavaScript Notes

### Prefer `const` for variable declaration

To declare variables that will not be changed, use `const`. If the variable will be changed, then use `let`.

**Bad:**

```javascript
let myVar1 = 1; // never changes
let myVar2 = 2;
let myVar3;

myVar2 = 5;

if (true) {
  myVar3 = 3;
}
```

**Good:**

```javascript
const myVar1 = 1; // never changes

let myVar2 = 2;
let myVar3;

myVar2 = 5;

if (true) {
  myVar3 = 3;
}
```

### Use short syntax for declaring methods in an object

**Bad:**

```javascript
const methods = {
  getValue: function() {},
  setValue: function() {},
};
```

**Good:**

```javascript
const methods = {
  getValue() {},
  setValue() {},
};
```

### Use arrow functions for callbacks

**Bad:**

```javascript
const arr = [1, 2, 3, 4, 5];

arr.forEach(function(item) {
  console.log(item);
});

setTimeout(function() {
  console.log('Yay!');
}, 1000);
```

**Good:**

```javascript
const arr = [1, 2, 3, 4, 5];

arr.forEach(item => {
  console.log(item);
});

setTimeout(() => {
  console.log('Yay!');
}, 1000);
```

### Always use strict equality and non-equality operators to avoid type issues

**Bad:**

```javascript
console.log(1 == '1'); // true
console.log(0 == false); // true
console.log('1' == true); // true
console.log('1' != 1); // false
```

**Good:**

```javascript
console.log(1 === '1'); // false
console.log(0 === false); // false
console.log('1' === true); // false
console.log('1' !== 1); // true
```

### Avoid saving `this` to a variable

If you need access to `this` from a callback function, then use arrow functions. They don't have their own `this` and take its value from the outside.

**Bad:**

```javascript
const obj = {
  values: [1, 2, 3, 4, 5],
  factor: 2,
  
  getMultipliedValues() {
    const self = this;
    
    return this.values.map(function(item) {
      return item * self.factor;
    });
  },
}

console.log(obj.getMultipliedValues()); // [2, 4, 6, 8, 10]
```

**Good:**

```javascript
const obj = {
  values: [1, 2, 3, 4, 5],
  factor: 2,

  getMultipliedValues() {    
    return this.values.map(item => item * this.factor);
  },

  // or
  // getMultipliedValues() {    
  //   return this.values.map(item => {
  //     return item * this.factor;
  //   });
  // },
}

console.log(obj.getMultipliedValues()); // [2, 4, 6, 8, 10]
```

### Use property value shorthand

If the properties have the same names as the variables, then use property value shorthand.

**Bad:**

```javascript
function getUser() {
  const name = 'Joe';
  const surname = 'Doe';

  return {
    name: name,
    surname: surname,
    isAdmin: false,
  };
}
```

**Good:**

```javascript
function getUser() {
  const name = 'Joe';
  const surname = 'Doe';

  return {
    name,
    surname,
    isAdmin: false,
  };
}
```
