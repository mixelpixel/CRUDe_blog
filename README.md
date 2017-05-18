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
 - **e** dit
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
1. gem 'simple_form', '~> 3.2'
2. gem 'bootstrap-sass', '~> 3.3'
3. gem 'ckeditor', '~> 4.1',

## [Rails Application](https://scotch.io/tutorials/build-a-blog-with-ruby-on-rails-part-1#toc-rails-application)
`rails new -T`  
`rails g model Post title:string body:text`  
`rake db:migrate`  
## [Installing Simple Form and Bootstrap-Sass](https://scotch.io/tutorials/build-a-blog-with-ruby-on-rails-part-1#toc-installing-simple-form-and-bootstrap-sass)
Add simple_form and bootstrap gems  
`$ bundle install`  
Set up bootstrap  
`rails generate simple_form:install --bootstrap`  
## [Setting up the Posts Controller and Views](https://scotch.io/tutorials/build-a-blog-with-ruby-on-rails-part-1#toc-setting-up-the-posts-controller-and-views)
`rails g controller Posts`  
Set up controller  
NOTE: There is an error in the code on the tutorial page. Should be:
```
  def create
    @post = Post.new(post_params)
    if @post.save
    ...
```
Create views: \_form.html.erb, new.html.erb, edit.html.erb, index.html.erb, & show.html.erb.
Configure routes  
##[Installing CKEditor](https://scotch.io/tutorials/build-a-blog-with-ruby-on-rails-part-1#toc-installing-ckeditor)
add ckeditor gem  
`bundle install`  
`rails generate ckeditor:install --orm=active_record --backend=carrierwave`  
`rake db:migrate`  
Set up CKEditor  

fin.
