Validations

* feature specs and model specs - (rarely use controller and view specs )
--- feature test will capture the controller and views
* feature tests slow --> use unit tests to check corner cases
* have single feature test checking for general failure
* checking the validity of a model
* individual (unit) tests for model elements 
-----e.g. expect(restaurant).to have(1).error_on(:name) vs not_to be_valid
---- rspec-collection_matchers
* implementing the validations
* more complex validations (length, capitals - regex \A[A-Z])
--- multiple errors
* adding the branching element to create (new and save)
* including the error messages in the form
* alternative messages
* css being added to form - using restaurants.css.scss
-- goldilocks - don't get too specific with css, and don't be too general



--------
(one to many)

* doing the check in update as well as new
