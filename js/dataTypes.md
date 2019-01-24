# Data types #


Primitive value types & reference value types
- JS has 2 kinds of variable types
- a fixed amount of memory is reserved after creation of every variables
- when variable is copied it's in-memory value is copied
- passing a variable to a function via call also creates a copy of that variable 

-----------

ECMAScript defines seven data types:
- primitives value types:
    * boolean
    * null
    * undefined
    * number
    * string
    * symbol (new in ES6)
- reference value types:
    * object
    
-----------------
### Primitive values
The in-memory value of primitive type is it's actual value. A primitive type can be stored in the fixed amount of available memory.
Primitive types as also known as scalar or simple type.

### Reference values
... can contains scalar values. Since the contents of reference type can not fit 
in the fixed amount of memory available for variable, the in-memory value 
of a reference type is the reference itself (a memory address).

-------------------
#### Boolean type
Represents a logical entity and can have two values: `true / false` 

---------------
#### null type
... is just null. Represents the intentional absence of any object value. 
`null` is not an identifier for a property of the global object, like undefined can be. 
Instead, `null` expresses a lack of identification, indicating that a variable points 
to no object. In APIs, null is often retrieved in a place where an object can be expected
 but no object is relevant.

--------------
#### undefined type
A variable that has not been assigned a value has the value undefined.

-----------------------
#### Number type
In ECMAScript, is only one number type (double-precision 64-bit binary format IEEE 754 value).
It means that numbers are between -(2^53 - 1 and (2^53 - 1). There is no specific type for integers.

--------
#### String type
JavaScript's String type is used to represent textual data. It is a set of 
"elements" of 16-bit unsigned integer values. 
Each element in the String occupies a position in the String. 
The first element is at index 0, the next at index 1, and so on. 
The length of a `String` is the number of elements in it.

`JavaScript strings are immutable.` 

This means that once a string is created, it is not possible to modify it. 
However, it is still possible to create another string based on an operation on the original string.

--------------
#### Symbol (new in ES6)
A Symbol is a unique and immutable primitive value and may be used as the key of an Object property.
More on MDN.

--------------
#### Object
In computer science, an object is a value in memory which is possibly referenced by an identifier.

In JavaScript, objects can be seen as a collection of properties. With the object literal syntax, a limited set of properties are initialized; then properties can be added and removed. Property values can be values of any type, including other objects, which enables building complex data structures. Properties are identified using key values. A key value is either a String or a Symbol value.

There are two types of object properties which have certain attributes: 
- data property - associates a key with a value and attributes
- accessor property - associates a key with one or two accessor functions (get and set) to retrieve or store a value 
