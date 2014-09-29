# Responding with XML and JSON (Rails Controllers)

By default, when we write the [controller action](http://edgeguides.rubyonrails.org/action_controller_overview.html#methods-and-actions) below, what is returned is given an [HTTP response header](http://en.wikipedia.org/wiki/List_of_HTTP_header_fields#Response_fields) of `Content-Type: text/html`, and any data (rendered by default from the view at `/app/views/users/index.html.erb`) is expected to be formatted as HTML.

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
    render json: @users # as simple as that!
  end
  
  def show
    @user = User.find(params[:id])
    render xml: @user   # as siple as that!
  end
end
```

We can also, within a single controller action, set up our application to [return different types of content based on what is requested](http://edgeguides.rubyonrails.org/action_controller_overview.html#rendering-xml-and-json-data)! Ie, we want to have a request to `http://our-app.co/users` to return HTML, but a request to:

1. `http://our-app.co/users.json`, or 
2. `http://our-app.co/users` with the HTTP *request* header of `Accept: application/json`

... to return JSON. Thus we would write our action:

```ruby
class UsersController < ApplicationController
  def index
    @users = User.all
    respond_to do |format|
      format.html # will, as usual, render the view at /app/views/users/index.html.erb
      format.json { render json: @users}
    end
  end
end
```

You can also connect some specific logic to a given request, as with:

```ruby
class UsersController < ApplicationController
  def feed
    respond_to do |format|
      format.html { render :users_base_feed, :layout => false }
      format.rss  { redirect_to feed_path(:format => :atom), :status => :moved_permanently }
      format.atom do
        @title   = "User Feed"
        @items   = User.order("updated_at desc")
        @updated = @items.first.updated_at unless @items.empty?
        
        render :layout => false
      end
    end
  end
end
```
