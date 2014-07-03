Code Smell --> Refactoring
===================

* obscure var/method names --> rename
* long method  --> extract method
* repetition (duplicated code) --> extract commonality
* nested control flow, e.g. ifs and loops --> extract method
* magic numbers (extract constants) --> extract constant
* responsibilities
* indentation

Always drive refactoring through tests to make sure you don't break things!

```ruby 

describe 'kitchen' do
  let(:contents) do
    [
      {name: 'Plate', owner: 'Jon'},
      {name: 'Cup', owner: 'Jon'},
      {name: 'Plate', owner: 'Sam'},
      {name: 'Cup', owner: 'Sam'},
    ]
  end
  it 'should print inventory by owner' do
    expect(self).to receive(:puts).with("Jon's Plate")
    expect(self).to receive(:puts).with("Jon's Cup")
    expect(self).to receive(:puts).with("Sam's Plate")
    expect(self).to receive(:puts).with("Jon's Cup")
    print_inventory_by_type contents
  end
end

```

Appendix
---------
* [Boolean Parameters](http://programmers.stackexchange.com/questions/147977/is-it-wrong-to-use-a-boolean-parameter-to-determine-behavior)

References
---------

* [http://en.wikipedia.org/wiki/Code_smell](http://en.wikipedia.org/wiki/Code_smell)
* [https://github.com/troessner/reek](https://github.com/troessner/reek)
* [https://github.com/troessner/reek/wiki/Code-Smells](https://github.com/troessner/reek/wiki/Code-Smells)
* [http://sourcemaking.com/refactoring/bad-smells-in-code](http://sourcemaking.com/refactoring/bad-smells-in-code)
