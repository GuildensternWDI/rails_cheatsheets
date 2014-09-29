# Using shoulda-matchers with ActiveRecord (Testing)

Once you have [set up RSpec and Capybara](testing_rspec_and_capybara.md) for you Rails app, you can use [thoughtbot's](http://thoughtbot.com/) `should-matcher` library ([Github](https://github.com/thoughtbot/shoulda-matchers), [Documentation](http://thoughtbot.github.io/shoulda-matchers)) to create simple, one-line tests for common Rails functionality in our models and controllers.

Most importantly, we can use `shoulda-matchers` to write unit tests for our models' **associations** and **validations**. While this might seem like simple boilerplate to begin with, it is a powerful setup to ensure basic functionality once we begin to add complex logic to our application.

### Examples:

Given the model `/app/models/user.rb` that has ...

We can write the follwing spec at `spec/models/user_spec.rb`:

```ruby
require 'spec_helper'

describe User do
  # associations
  it { should belong_to(:group)  }
  it { should have_one(:account) }
  it { should have_many(:feeds)  }
  it { should have_many(:feeds).through(:stars) }
  
  # validations
  it { should validate_presence_of(:email)        }
  it { should validate_uniqueness_of(:email)      }
  it { should validate_presence_of(:name)         }
  it { should validate_confirmation_of(:password) }
end
```

This spec will pass when we write the model so that:

```ruby
class User < ActiveRecord::Base

end
```
