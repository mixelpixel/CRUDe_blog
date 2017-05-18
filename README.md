# C.R.U.D.
I am following this tutorial:
1. https://scotch.io/tutorials/build-a-blog-with-ruby-on-rails-part-1  
2. https://scotch.io/tutorials/build-a-blog-with-ruby-on-rails-part-2  
...mostly because I wanted to quickly learn how to set up a blog using CKEditor.  
Having finished this tutorial, I moved on to:  
3. http://guides.rubyonrails.org/v4.2/getting_started.html

## My aim is to build a CRUD blog with text editing, hence "CRUDe"
 - **C** reate
 - **R** ead
 - **U** pdate
 - **D** estroy
 - **e** dit text with [CKEditor](http://www.rubydoc.info/gems/ckeditor/4.2.0).  
..some thoughts on [CRUD and REST](https://softwareengineering.stackexchange.com/questions/120716/difference-between-rest-and-crud) (Representational State Transfer)  

### I initialized this git repository locally and got started.
1. After finishing part one of the tutorial I decided to push the repo to github.
2. Per: https://help.github.com/articles/adding-an-existing-project-to-github-using-the-command-line/

### Ruby and Rails versions, working with macOS Sierra
```
$  ruby -v
ruby 2.3.0p0 (2015-12-25 revision 53290) [x86_64-darwin16]
$  rails -v
Rails 4.2.0
```
# [Part One](https://scotch.io/tutorials/build-a-blog-with-ruby-on-rails-part-1)

## [Rails Application](https://scotch.io/tutorials/build-a-blog-with-ruby-on-rails-part-1#toc-rails-application)
1. `rails new -T`  
2. `rails g model Post title:string body:text`  
3. `rake db:migrate`  
## [Installing Simple Form and Bootstrap-Sass](https://scotch.io/tutorials/build-a-blog-with-ruby-on-rails-part-1#toc-installing-simple-form-and-bootstrap-sass)
4. Add simple_form and bootstrap gems to Gemfile  
5. `$ bundle install`  
6. Set up bootstrap  
  - add bootstrap requirement to app/assets/javascripts/application.js  
  - Rename app/assets/stylesheets/application.**css** to  
           app/assets/stylesheets/application.**scss**
  - add @imports to Sass (.scss) file.
7. `rails generate simple_form:install --bootstrap`  
## [Setting up the Posts Controller and Views](https://scotch.io/tutorials/build-a-blog-with-ruby-on-rails-part-1#toc-setting-up-the-posts-controller-and-views)
8. `rails g controller Posts`  
9. Set up controller  
  - NOTE: There is an error in the code on the tutorial page.  
    app/controllers/posts_controller.rb should be:
    ```
      def create
        @post = Post.new(post_params)
        if @post.save # <----- tutorial has (post_params) here
        ...
    ```
  - and:
    ```
      def update
        if ...
          redirect_to post_path(@post) # <--- singular
      ...
    ```
10. Create /app/views/: \_form.html.erb, new.html.erb, edit.html.erb, index.html.erb, & show.html.erb.
11. Configure /app/config/routes.rb  
## [Installing   CKEditor](https://scotch.io/tutorials/build-a-blog-with-ruby-on-rails-part-1#toc-installing-ckeditor)
12. add ckeditor gem  
13. `bundle install`  
14. `rails generate ckeditor:install --orm=active_record --backend=carrierwave`  
15. `rake db:migrate`  
16. Set up CKEditor
  - add ckeditor requirement to app/assets/javascripts/application.js  
  - Create a directory called ckeditor in app/assets/javascripts, then create a new file called config.js

Part 1 fin.

# [Part Two](https://scotch.io/tutorials/build-a-blog-with-ruby-on-rails-part-2 )
## Enable Authentication Using Devise.
1. Add Devise gem to your Gemfile: `gem 'devise', '3.5.2'`  
2. `bundle install`  
3. `rails g devise:install`  
Always read this stuff:  
```
$  rails g devise:install
Running via Spring preloader in process 18743
Expected string default value for '--test-framework'; got false (boolean)
Expected string default value for '--helper'; got true (boolean)
      create  config/initializers/devise.rb
      create  config/locales/devise.en.yml
===============================================================================

Some setup you must do manually if you haven't yet:

  1. Ensure you have defined default url options in your environments files. Here
     is an example of default_url_options appropriate for a development environment
     in config/environments/development.rb:                                         # <---- THIS
                                                                                    # <---- and
       config.action_mailer.default_url_options = { host: 'localhost', port: 3000 } # <---- THIS

     In production, :host should be set to the actual host of your application.

  2. Ensure you have defined root_url to *something* in your config/routes.rb.      # <---- DONE
     For example:

       root to: "home#index"

  3. Ensure you have flash messages in app/views/layouts/application.html.erb.      # <---- TO DO
     For example:

       <p class="notice"><%= notice %></p>
       <p class="alert"><%= alert %></p>

  4. If you are deploying on Heroku with Rails 3.2 only, you may want to set:       # <---- NOPE

       config.assets.initialize_on_precompile = false

     On config/application.rb forcing your application to not access the DB
     or load models when precompiling your assets.

  5. You can copy Devise views (for customization) to your app by running:          # <---- TO DO

       rails g devise:views

===============================================================================
```
4. update config/environments/development.rb with  
  `config.action_mailer.default_url_options = { host: 'localhost', port: 3000 }`  
5. update app/views/layouts/application.html.erb with  
  ```
  <p class="notice"><%= notice %></p>
  <p class="alert"><%= alert %></p>
  ```
6. `rails g devise Admin`  
7. `rake db:migrate`
8. `rails g devise:views admin`  
9. modify views/admins/registrations/edit.html.erb  
10. modify views/admins/registrations/new.html.erb  
11. modify views/admins/sessions/new.html.erb  
12. modify views/admins/shared/\_links.html.erb  
13. Uncomment line 211 of Devise initializer; config/initializers/devise.rb  
    - change `false` to `true`  
14. Check out: http://localhost:3000/admins/sign_in  
15.   

## Enable Image Uploading.
