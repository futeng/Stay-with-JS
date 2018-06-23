### 5.1 Name Binding

> In programming languges, name binding is the association of entities(data and/or code) with an identifiers. An identifier bound to an object is said to  reference that object.
>
> Binding is intimately connected with scoping, as scope determines which names bind to which object - at which locations in the program code(Lexical) and in which one of the possible execution paths(Dynamic)
>
> from: https://en.wikipedia.org/wiki/Name_binding

#### 5.1.1 Binding time

- The bindings of names before the program is run is called **static/early**;
- bindings performed as the program runs are **dynamic(late/virtual)**.

#### 5.1.2 Rebinding vs Mutation

```java
LinkedList<String> list; // an identifir 'list' bindding/reference to nothing.
list = new LinkedList<String>(); // 'list' rebound to reference an object(a linked list of string). 
list.add("foo"); // 'list' is then mutated, adding a string to the list
list = null; // 'list' is rebound to null.
```