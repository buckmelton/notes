# Buck's Rails Notes

## Theory
- Rails has two guiding principles:
  - Keep your code DRY (Don't Repeat Yourself)
  - Convention Over Configuration
- Keep re-reading RoR Getting Started guide to strengthen knowledge


## Practice

### Install Rails
`$ gem install rails -v 4.2.2`

### Create a new app:
  >\>rails new APP_NAME --skip-spring --database=postgres --skip-test-unit

  - according to lecturer, spring is more trouble than it's worth
  -  rails uses sqlite by default, but we want postgres
  -  by default the javascript framework is jquery, but you could do e.g. --javascript=react
  - skipping test-unit cuz we're using rspec

#### If you need to make changes to default application gems
- Open `Gemfile` with editor
- Make changes
- Install new/changed gems:
`$ cd <APP_NAME>`
`$ bundle install`

### Run server
Rails comes with a command-line program, or *script*, that runs a *local* web server to assist in developing our application.

On a local system, just run  
`rails server`.

On cloud-based dev env (e.g. Cloud9), need to supply add'l *IP binding address* and *port number* to tell Rails server the address it can use to make the application visible to the outside world.  Cloud9 uses `$IP` and `$PORT` to assign them dynamically.  
Make sure you're in the application directory.  
`$ rails server -b $IP -p $PORT`

To shut down server: `CTRL-C`

#### When an app runs, what happens sequentially is:

- environment.rb
  - which loads boot.rb
    - which loads application.rb
    - application file runs and starts to configure the environment
      - runs one of the environment config files (e.g. development.rb, production.rb, test.rb)
      - then run all the initializers, then the app is up and running
      
- browser sends request
- received by a web server
- which passes the request to the Rails *router* (`config/routes.rb') which figures out which controller
- and passes the request to a Rails *controller*
- the *controller* interacts with a *model*
- the *controller* renders the *view* and returns the complete web page to the browser as HTML
      
### View App in Browser
On a local server, go to http://localhost:3000/.  
On Cloud9, go to Share and click on the Application address.  
You should see the default Rails page.

### Create your first Controller#action and point root route to it
For example:  
- In `application_controller.rb` create `def hello` action to render text `hello, world!`  
- Then edit `config/routes.rb` to have `root 'application#hello'`

### Scaffolding
The quickest easiest way to create an app is to use scaffolding, e.g. to use scaffolding create a "Micropost" app (i.e. a Twitter clone) with Users and Microposts:
```
> rails generate scaffold User name:string email:string
> bundle exec rake db:migrate

> rails generate scaffold Micropost content:text user_id:integer
> bundle exec rake db:migrate
```
The above commands added resource lines to `config/routes.rb`
You can see all the generated routes: `> be rails routes'

Fire up server `rails server -b $IP -p $PORT`
Visit any of the routes e.g. `localhost:3000/users`
You can replace the root route from before (`application#hello`) in routes.rb with `users#index`

### Routes:
  - When a request comes in, it goes to config/routes.rb
  - routes.rb starts with Rails.application.routes.draw do

  - get '/info' => 'static#info'
    - Here's the pattern to match on (/info), go to controller and action (controller 'static', action 'info')

### Naive creation of a Rails app
- If you start server:
  >\>be rails s
  - go to localhost, you will get database doesn't exist error

- Shut down server
  >\>be rake db:create db:migrate  
  >\>be rails s
- Should get generic Rails home page
- Now try to go to our route
- localhost:3000/info
- You'll get uninitialized StaticController cuz we havent made the controller
  >\>be rails generate controller static info
- anything listed after controller name will be created as an action
- Now that controller is made, go to localhost:3000/info, you'll get missing view error
- Make views/static/info.html.erb, put in 'hello'
- Now localhost:3000/info gets 'hello'

### Gem tips
From the gemfile, remove gems you arent using, these will be reflected when you generate controllers.  
E.g. if you leave in coffeescript gem, when you generate controller a coffeescript file will be generated.

Three ways to specify gem version in Gemfile:
- gem 'coffee-rails'  '4.1.0'     # exact
- gem 'uglifier'      '>= 1.3.0'  # install latest as long as it's >= 1.3.0
- gem 'coffee-rails'  '-> 4.0.0'  # install latest that's newer than 4.0.0 but not newer than 4.1, i.e. only minor point releases

### Asset Pipeline
  - In Sinatra, if you had js or css you would just add another script or link to the erb file
  - In Rails, you will never add a script or stylesheet at all, you will always have one stylesheet and one js file.
  - The way you add functionality is you add those tools and scripts to your compiled assets, your asset pipeline.

  - In development youll see multiple script/link tags, but not in production

### Controllers
  - ApplicationController
    - any helpers you put in here, through inheritance, gets inherited by all controllers.

    - good place to put filters e.g. before_action :ensure_logged_in!
    
### Rails Console
Different from ruby console.  
Rails console allows you to verify the auto-generated ActiveRecord associations and the consequent objects.
`be rails console`



