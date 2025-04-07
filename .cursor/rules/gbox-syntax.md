# Gbox Syntax Rules

## Description
Use these rules when analyzing or generating Gbox script code to ensure correct syntax and language features usage.

## Files
*.gb, *.gbz

## Reference Files
@doc/gbox_syntax.md

## Rules

### Syntax Understanding
- Refer to the complete syntax documentation in @doc/gbox_syntax.md for details
- Understand that Gbox scripting has its own unique syntax despite resembling C/C++
- Recognize and properly use Gbox-specific operators and expressions

### Variable Declaration
- All variable declarations must specify a type (int, float, string, obj, vec2, etc.)
- Member variables must follow specific naming conventions with proper prefixes
- Example: `int m_nCount`, `string m_sName`, `obj m_pShape`, `vec2 m_vPos`
- Always initialize variables when appropriate to prevent undefined behavior

### Class Structure
- All classes must inherit from either GObj (base class) or another valid Gbox class
- Class definition syntax is: `class MyClass : ParentClass {}`
- Classes can also inherit styles (a Gbox-specific concept)
- Example: `class MySprite : GObjShape, MyCustomStyle {}`

### Function Syntax
- Functions must have return types declared (use `void` for no return value)
- Function parameters can have default values
- Example: `int Calculate(int x, int y = 10) { return x + y; }`

### Object Creation and Management
- Understand the three ways to create objects:
  1. Using `new` keyword: `obj m_pObj = new GObj;`
  2. Using direct class declaration: `GObjShape m_pShape;`
  3. Using dynamic creation: `obj p = NewObj("GObjShape", this);`
- Remember that objects need proper deletion: `p.DelThis()` or `SafeDelObj(p)`

### Array and Dictionary Handling
- Arrays are created with parentheses: `var arr = (1, 2, 3, "hello");`
- Understand VID arrays and their accessor methods: `v.vset("key", value);`
- Use dictionary methods correctly: `vdic.svSet("key", value);`

### Styles Usage
- Correctly define and apply styles as a code reuse mechanism
- Typed styles need type specification: `style<GObjShape> MyStyle {}`
- Remember that styles can be inherited by classes but must come after the parent class

### Error Handling
- Use proper error handling with `catch` blocks and `Abort()`
- Access error information via `_err`, `_erragv`, and `_errinfo` 