# Responding with XML and JSON (Rails Controllers)

By default, when you write the controller action below, what is returned is given an [HTTP response header](http://en.wikipedia.org/wiki/List_of_HTTP_header_fields#Response_fields) of `Content-Type: text/html`, and any data (rendered by default from the view at `app/views/users/index.erb`) is expected to be formatted as HTML.

```ruby
class UsersController < ApplicationController
  def index
    @users = User.all
  end
end
```

But, as discussed in the Rails Guide ([Layouts and Rendering](http://guides.rubyonrails.org/layouts_and_rendering.html#rendering-json)), you can instead have it render JSON or XML, by writing it as one of the below:

```ruby
class UsersController < ApplicationController
  def index
    @users = User.all
    render xml: @users 
  end
  
  def show
    @user = User.find(params[:id])
    render json: @user
  end
end
```

You can also, within a single controller action
