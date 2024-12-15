# Antlr C++ visitor pattern

The visitor pattern implementation in Antlr is hard to use, to the point that it's infeasible to use in any serious project. The main cause:

**Every visitor method in the visitor class returns `std::any`.**

This makes Antlr's visitor pattern usage infeasible for generating ASTs because:

1. Any non-trivial syntax tree classes will have a hierarchy. Thus, polymorphism is essential (i.e. returning/passing a child class from/to a function that expects a parent class). 
1. Polymorphism in C++ is possible only by pointers (i.e. a parent pointer can also point to a child instance, this isn't possible with regular types or references).
1. The memory safe way of using pointers in C++ is with smart pointers. 
1. `std::unique_ptr` is a preferred smart pointer than `std::shared_ptr`. Some guides/organizations don't use `std::shared_ptr` at all unless necessary.
1. `std::unique_ptr` is non-copyable. Returning a `std::unique_ptr` to an AST node instance from a visitor function causes compiler error, since `std::any` is copyable, and `std::unique_ptr` is not.
1. There is no way in Antlr that enables users provide custom return types. There is an [open proposal](https://github.com/antlr/antlr4/issues/2348) for several years, but it never materialized.
