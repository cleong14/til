# Go Automatically Handles Conversion Between Values and Pointers for Method Calls

Methods can be defined for either pointer or value receiver types.

[Go automatically handles conversion between values and pointers for method calls](https://gobyexample.com/methods).
You may want to use a pointer receiver type to avoid copying on method calls or
to allow the method to mutate the receiving struct.
