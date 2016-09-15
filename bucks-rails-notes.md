## Buck's Rails Notes

### Theory
- Rails has two guiding principles:
  - Keep your code DRY (Don't Repeat Yourself)
  - Convention Over Configuration
- Keep re-reading RoR Getting Started guide to strengthen knowledge


### Practice

#### Creating a new app:
  >\>rails new APP_NAME --skip-spring --database=postgres --skip-test-unit

  - according to lecturer, spring is more trouble than it's worth
  -  rails uses sqlite by default, but we want postgres
  -  by default the javascript framework is jquery, but you could do e.g. --javascript=react
  - skipping test-unit cuz we're using rspec

#### When an app runs, what happens sequentially is:

- environment.rb
  - which loads boot.rb
    - which loads application.rb
    - application file runs and starts to configure the environment
      - runs one of the environment config files (e.g. development.rb, production.rb, test.rb)
      - then run all the initializers, then the app is up and running

#### Routes:
  - When a request comes in, it goes to config/routes.rb
  - routes.rb starts with Rails.application.routes.draw do

  - get '/info' => 'static#info'
    - Here's the pattern to match on (/info), go to controller and action (controller 'static', action 'info')

#### Naive creation of a Rails app
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

#### Gem tips
From the gemfile, remove gems you arent using, these will be reflected when you generate controllers.
E.g. if you leave in coffeescript gem, when you generate controller a coffeescript file will be generated.

#### Asset Pipeline
  - In Sinatra, if you had js or css you would just add another script or link to the erb file
  - In Rails, you will never add a script or stylesheet at all, you will always have one stylesheet and one js file.
  - The way you add functionality is you add those tools and scripts to your compiled assets, your asset pipeline.

  - In development youll see multiple script/link tags, but not in production

#### Controllers
  - ApplicationController
    - any helpers you put in here, through inheritance, gets inherited by all controllers.

    - good place to put filters e.g. before_action :ensure_logged_in!



