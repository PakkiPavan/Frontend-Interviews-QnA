**Input/Output Questions**

**Question:1**

```javascript
let numbers=[1,2,3,4,5,6]
numbers.forEach(num=>{
  if(num===2) return;
  console.log(num);
})
```


**Question:2**

```javascript
const user={
  name:"Alice",
  address:{
    city:"Wonderland",
    zip:"12345"
  }
};
const user2={...user};
user2.address.zip="456";
// what is output of user.address.zip?
// Output is "456"
```

**Explanation**  
- In above code, after using the spread operator (...user), the user2 object is created as a shallow copy of the user object.
- However, since the address property is an object itself, the shallow copy only copies the reference to the original address object, not a deep copy of its contents.
- Shallow Copy: The spread operator (...user) only copies the top-level properties.
- Since address is an object (a reference type), both user and user2 will still refer to the same address object in memory.
- Since both user and user2 share the same address object, the change made to user2.address.zip will also reflect in user.address.zip.
- Both user and user2 will have zip equal to "456" because they share the same reference to the address object. The original zip value "12345" is overwritten.


**Question:3**

```javascript
const obj={
  a:function(){
    console.log(this);
  },
  b:()=>{
    console.log(this);
  }
};

// What is output of obj.a() and obj.b()?
// Output for obj.a() will print {a: f(), b: ()=>{ console.log(this); } }
// Output for obj.b() will print window object
```

**Exaplnation:**

- **Regular functions (a):**
  - The value of this depends on how the function is called.
  - When a regular function is called as a method on an object, this refers to the object that called the method.
  - In this case, this refers to the obj object.
- **Arrow functions (b):**
  - Arrow functions do not have their own this.
  - Instead, they inherit this from the surrounding lexical context (where the function is defined).
  - In above example, b is defined in the global scope (or whatever surrounding scope exists), so this will refer to the global object in non-strict mode (window in browsers) or undefined in strict mode.

```obj.a()```  
- Since a is a regular function and is called as obj.a(), the this inside a refers to the obj object. So, console.log(this) will output the obj object.

```obj.b()```
- Since b is an arrow function, it doesn't have its own this context.
- It inherits this from the surrounding lexical environment, which is the global context in this case. Therefore:
  - In non-strict mode, this will refer to the global object (window in browsers).
  - In strict mode, this will be undefined.

**Summary**  
- obj.a() will log the obj object.
- obj.b() will log the global object (window in non-strict mode) or undefined (in strict mode).


**Question:4**

```javascript
let a={}
let b=a;
a.x=2;
console.log(b.x) // Output: 2
```


**Question:5**

```javascript
function customFunction(){
  console.log(x);// Output:1
  var x=20;
  console.log(x); // Output:2
}
customFunction();
console.log(x);// Output: 3

// Output:1 -> undefined
// Output:2 -> 20
// Output:3 -> ReferenceError: x is not defined
```
