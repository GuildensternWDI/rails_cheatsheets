# Using `shoulda-matchers` with ActiveRecord (Testing)

Once we have [set up RSpec and Capybara](testing_rspec_and_capybara.md) for you Rails app, we can use [thoughtbot's](http://thoughtbot.com/) `should-matcher` library ([Github](https://github.com/thoughtbot/shoulda-matchers), [Documentation](http://thoughtbot.github.io/shoulda-matchers)) to create simple, one-line tests for common Rails functionality in our models and controllers.

Most importantly, we can use `shoulda-matchers` to write unit tests for our models' **associations** and **validations**. While this might seem like simple boilerplate to begin with, it is a powerful setup to ensure basic functionality once we begin to add complex logic to our application.

### Installation

We can install `shoulda-matchers` by including the gem in our Gemfile:

```ruby
group :test do
  gem 'shoulda-matchers', require: false
end
```

... and then requiring it our `/spec/rails_helper.rb` file:

```ruby
...
require 'rspec/rails' # after here!
require 'shoulda/matchers'
```

### Example

Given the model `/app/models/user.rb` that has the attributes email, name and password, and relationships with the models Group, Account, and Feeds, such that:
  - a user belongs to a group (ie, a user has one group, and a group has many users),
  - a user has a single account they are related to if they are paying subcribers,
  - a user has many feeds that they have created, and
  - a user has many more feeds that they have starred.

We can write the following spec at `spec/models/user_spec.rb`:

```ruby
require 'rails_helper'

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
