# C.R.U.D.
I am following this tutorial:
1. https://scotch.io/tutorials/build-a-blog-with-ruby-on-rails-part-1  
2. https://scotch.io/tutorials/build-a-blog-with-ruby-on-rails-part-2  
...mostly because I wanted to quickly learn how to set up a blog using CKEditor.  
Having finished this tutorial, I moved on to:  
3. http://guides.rubyonrails.org/v4.2/getting_started.html

# My aim is to build a CRUD blog with text editing, hence "CRUDe"
 - **C** reate
 - **R** ead
 - **U** pdate
 - **D** estroy
 - **e** dit text with [CKEditor](http://www.rubydoc.info/gems/ckeditor/4.2.0).
 - some thoughts on [CRUD and REST](https://softwareengineering.stackexchange.com/questions/120716/difference-between-rest-and-crud) (Representational State Transfer)  

## I initialized this git repository locally and got started.
1. After finishing part one of the tutorial I decided to push the repo to github.
2. Per: https://help.github.com/articles/adding-an-existing-project-to-github-using-the-command-line/
 - (skipping steps 4, 5, & 6)
 - `git push -u origin master`

### Ruby and Rails versions, macOS Sierra
```
$  ruby -v
ruby 2.3.0p0 (2015-12-25 revision 53290) [x86_64-darwin16]
$  rails -v
Rails 4.2.0
```
### System dependencies
- gem 'simple_form', '~> 3.2'
- gem 'bootstrap-sass', '~> 3.3'
- gem 'ckeditor', '~> 4.1',

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
        if @post.save
        ...
    ```
10. Create /app/views/: \_form.html.erb, new.html.erb, edit.html.erb, index.html.erb, & show.html.erb.
11. Configure /app/config/routes.rb  
##[Installing CKEditor](https://scotch.io/tutorials/build-a-blog-with-ruby-on-rails-part-1#toc-installing-ckeditor)
12. add ckeditor gem  
13. `bundle install`  
14. `rails generate ckeditor:install --orm=active_record --backend=carrierwave`  
15. `rake db:migrate`  
16. Set up CKEditor
  - add ckeditor requirement to app/assets/javascripts/application.js  
  - Create a directory called ckeditor in app/assets/javascripts, then create a new file called config.js

fin.
