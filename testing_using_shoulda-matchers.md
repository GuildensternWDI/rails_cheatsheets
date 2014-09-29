# Using shoulda-matchers with ActiveRecord (Testing)

Once you have [set up RSpec and Capybara](testing_rspec_and_capybara.md) for you Rails app, you can use [thoughtbot's](http://thoughtbot.com/) `should-matcher` library ([Github](https://github.com/thoughtbot/shoulda-matchers), [Documentation](http://thoughtbot.github.io/shoulda-matchers)) to create simple, one-line tests for common Rails functionality in our models and controllers.

Most importantly, we can use `shoulda-matchers` to write unit tests for our models' **associations** and **validations**.

For example:
