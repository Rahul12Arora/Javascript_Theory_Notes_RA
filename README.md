# Javascript_Theory_Notes
Javascript_Theory 140322

<h2>Scope & Var, let & const</h2>
A scope of a parameter is a certain region of a programm or its bound where it can be access or recognised

<h3>Scope types</h3>
1.) Global scope</br>
2.) Function Scope</br>
3.) Block Scope</br>

**var is block scoped but let & const are block scoped**

<h3>Shadowing</h3>

**Shadowing is when an inner variable overrides an outer variable of the same name inside the inner variable's scope**

```
function test(){
    var a = "hello"
    let b = "goodbye"
    
    if(true){
        let a = "hi"    // Shadowing
        var b = "bye"   // Illegal shadowing
    }
}
```

<h3>Declaration</h3>

**let & const cannot be re declared in the same scope**
**var can be redeclared in the same scope**

**const cannot be declared without initialization, once initialized it cannot be re-initialized**

<h2>Hoisting - An execution context is created</h2>

<h3>Creation Phase</h3>
<li>Creates a Global/Window Object</li>
<li>Creates an Execution Phase</li>


  
