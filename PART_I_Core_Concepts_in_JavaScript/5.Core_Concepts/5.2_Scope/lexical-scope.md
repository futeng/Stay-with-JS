# Lexical Scoping

> JavaScript uses lexical scoping. This means that functions are executed using the variable scope that was in effect when they were defined, not the variable scope that is in effect when they are invoked.
>
> In order to implement lexical scoping, the internal state of a JavaScript function object must include not only the code of the function but also a reference to the current scope chain. 

> Tokenizing/Lexing: Bring up a string of characters into meaningful chunks. For instance, consider the program `var a = 2;` This program would likely broken up into the following tokens: var , a , = , 2;