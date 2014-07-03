Code Smell --> Refactoring
===================

* long method  --> extract method
* obscure var/method names --> rename
* repetition (duplicated code) --> extract commonality
* nested control flow, e.g. ifs and loops --> extract method
* magic numbers (extract constants) --> extract constant
* responsibilities
* indentation

Always drive refactoring through tests to make sure you don't break things!

References
---------

* [http://en.wikipedia.org/wiki/Code_smell](http://en.wikipedia.org/wiki/Code_smell)
* [https://github.com/troessner/reek](https://github.com/troessner/reek)
* [http://sourcemaking.com/refactoring/bad-smells-in-code](http://sourcemaking.com/refactoring/bad-smells-in-code)
