# Steps to creating a Rails application

###Starting a New Rails Project

* [ ] Create a new Rails Project
 
 ```
$ rails new AppName -T -d postgresql
 ```
 
* [ ] Switch to its folder

 ```
$ cd AppName
 ```
 
* [ ] Install the gem dependencies 

 ```
$ bundle install
 ```
 
* [ ] Start up web server 
 ```
$ rails s
 ```
 
 
###Setup Rails DB
* [ ] Create a new model
 ```
$ rails g model fish species:string name:string age:integer
 ```
* [ ] Create the db
 ```
$ rails db:create
 ```
* [ ] Initialize the DB
 ```
$ rails db:migrate
 ```
 
 
###Setup Rails File Structure "Hello Rails"

* [ ] Create a new controller
 ```
$ bin/rails generate controller Welcome index
 ```
* [ ] Insert "Hello Rails" into app/views/welcome/index.html.erb

#### Set the Application Home Page

* [ ] Tell Rails where your actual home page is located in config/routes.rb
```
Rails.application.routes.draw do
  get 'welcome/index'
  root 'welcome#index'
end
 ```
* [ ] Run server, view "Hello Rails" message

###  Set the Controllers and Views

* [ ] Set up Routes for each model
* [ ] In controller setup ISNECUD
* [ ] In view setup correspoding pages for each NECUD

```
#Sample Controller
class OwnersController < ApplicationController

  def index
    @owners = Owner.all
  end

  def show
    owner_id = params[:id]
    @owner = Owner.find_by(id: owner_id)
  end

  def new
    @owner = Owner.new
  end

  def create
    owner = Owner.new(owner_params)
    if owner.save
      redirect_to owner_path(owner)
    else
      flash[:error] = owner.errors.full_messages.join(", ")
      redirect_to new_owner_path
    end
  end

  def edit
    owner_id = params[:id]
    @owner = Owner.find_by(id: owner_id)
  end

  def update
    owner_id = params[:id]
    owner = Owner.find_by(id: owner_id)
    if owner.update(owner_params)
      redirect_to owner_path(owner)
    else
      flash[:error] = owner.errors.full_messages.join(", ")
      redirect_to edit_owner_path(owner)
    end
  end

  def destroy
    owner_id = params[:id]
    owner = Owner.find_by(id: owner_id)
    owner.destroy
    redirect_to owners_path
  end

  private
  def owner_params
    params.require(:owner).permit(:first_name, :last_name, :email, :phone)
  end
end
 ```

###Getting Up and Running w/ CRUD

* [ ] Create a new resource and add it to config/routes.rb
```
Rails.application.routes.draw do
  resources :articles
  root 'welcome#index'
end
 ```
* [ ] Run 'bin/rails routes' to view defined routes for all the standard RESTful actions.

* [ ] Create a controller called ArticlesController
```
$ bin/rails generate controller Articles
```
* [ ] Define a new method inside the controller. In app/controllers/articles_controller.rb and the ArticlesController class, define the new method
```
class ArticlesController < ApplicationController
  def new
  end
end
```
* [ ] Add the view. Create a new file at app/views/articles/new.html and write "New Article"