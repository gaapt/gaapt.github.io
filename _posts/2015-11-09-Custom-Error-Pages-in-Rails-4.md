---
layout: post
title: Custom Error Pages in Rails 4
---
Before anything, we must delete the default error pages:

```bash
rm public/404.html
```

Then, create the errors controller at `app/controllers/errors_controller.rb` for each error status code:

```ruby
class ErrorsController < ApplicationController
 
  def not_found
    render :status => 404
  end
 
  def unacceptable
    render :status => 422
  end
 
  def internal_server_error
    render :status => 500
  end
 
end
```

In `app/views/errors`, add views with your desired message:

```erb
#app/views/errors/not_found.html.erb
Sorry, this page was not found 

#app/views/errors/unnacceptable.html.erb
Sorry, our server was unable to process the contained instructions

#app/views/errors/internal_server_error.html.erb
Sorry, our server had an error.
```

Alternatively, you can create a view `app/views/layouts/error.html.erb` to handle custom errors:

``` erb
<html>
  <body>
    <div class="error_container">
        <%= yield %>
    </div>
  </body>
</html>
```

Now, it is necessary to route exceptions to the application router in `config/environments/production.rb`:

```ruby
config.exceptions_app = self.routes
```

With that, we update the routing configuration in `config/routes.rb` to direct error page requests to the `show` action of the errors controller: 

``` ruby
  get "/404", :to => "errors#not_found"
  get "/422", :to => "errors#unacceptable"
  get "/500", :to => "errors#internal_server_error"

```
