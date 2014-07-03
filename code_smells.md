Code Smell --> Refactoring
===================

* obscure var/method names --> rename
* long method  --> extract method
* repetition (duplicated code) --> extract commonality
* nested control flow, e.g. ifs and loops --> extract method
* magic numbers (constants) --> extract constant
* responsibilities
* indentation

Always drive refactoring through tests to make sure you don't break things!

Appendix
---------
* [Boolean Parameters](http://programmers.stackexchange.com/questions/147977/is-it-wrong-to-use-a-boolean-parameter-to-determine-behavior)

References
---------

* [http://en.wikipedia.org/wiki/Code_smell](http://en.wikipedia.org/wiki/Code_smell)
* [https://github.com/troessner/reek](https://github.com/troessner/reek)
* [https://github.com/troessner/reek/wiki/Code-Smells](https://github.com/troessner/reek/wiki/Code-Smells)
* [http://sourcemaking.com/refactoring/bad-smells-in-code](http://sourcemaking.com/refactoring/bad-smells-in-code)
