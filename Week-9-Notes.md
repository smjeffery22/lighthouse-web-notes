# **Jeffery Park's LHL Week 9 Notes**

## **Table of Contents**

- [DAY 1 COMPASS NOTES](#day1comp)
- [DAY 2 COMPASS NOTES](#day2comp)
- [DAY 3 COMPASS NOTES](#day3comp)
- [DAY 4 COMPASS NOTES](#day4comp)

<a id="day1comp"></a>
## **DAY 1 COMPASS NOTES**

## ACTIVE RECORDS (AR)

  - AR as part of Rails for the purpose of defining *Database Models*
    - Allow the web app to easily work with a *SQL database using Classes*
  
  - Each *AR Class* (a.k.a. Mdel) corresponds to an *existing table in the database*
    - Provides *attributes* that map to each *column/field* in the table
    - Allows *CRUD* records in that table using that Class and its instances

  ```ruby
  # Executes the following SELECT and returns an instance attributes for that record:
  #   SELECT * FROM users WHERE email = 'bob@loblaw.com' LIMIT 1;
  user = User.find_by(email: 'bob@loblaw.com')

  # Reads an attribute (like an attr_reader)
  user.id # => 5

  # These are just like an attr_writers, performing changes in memory (no UPDATE sql)
  user.name  = 'Bob'
  user.email = 'bob@loblaw.org'

  # Executes the following UPDATE statement:
  #   UPDATE users SET name = 'Bob', email = 'bob@loblaw.org' WHERE id = 1;
  # (Assuming id of record was 1)
  user.save
  ```

  - *User* model connect to the *users* table in the database
  - If the table has two fields, *name* and *email* (aloing with *id* primary key)
    - AR allows to get/set these fields on a given instance of User

## ACTIVE RECORDS - RAILSGUIDES

  - AR is **M** of *Model-view-controller (MVC)*
    - MVC is commonly used for developing *user interfaces (UI)*
      - Devide the related program logic into 3 interconnected elements
  
  - **Model**
    - Application's dynamic data structure, independent of the UI
    - *Directly manages the data, logic and rules of the application*
    - Responsible for managing the data of the application
      - Receives user input from the controller
  
  - **View**
    - *Representation of information* such as a chart, diagram or table
      - Multiple views of the same information are possible
        - i.e. bar chart, tabular view
    - Renders presentation of the model in a particular format

  - **Controller**
    - Accepts input and converts it to commands for the model or view
    - Responds to the user input and performs interactions on the data model objects
      - Receives input and pass it to the model

### ACTIVE RECORD PATTERN

  - In AR, objects carry both *persistent data* and *behaviour* which operates on that data
    - *persistent data:* data that is not frequently accessed/manipulated (i.e. static)
  - Ensuring data access logic as part of the object will educate users of that object on how to write/read from the database

### OBJECT RELATIONAL MAPPING (ORM)

  - A technique that connects the rich objects of an application to tables in a relational database management system
  - Using ORM, the properties and relationships of the objects in an application can be easily stored and retrieved from a database
    - Without writing SQL statements and less database access code

### CONVENTION OVER CONFIGURING IN AR

  - Following the conventions adopted by Rails, little configuration to none is required when creating AR models
  - Explicit configuration only needed when the standard convention cannot be followed

#### NAMING CONVENTIONS

  - Default naming conventions used by AR to find out how the *mapping between models and database tables* should be created
  
  - **Model Class**
    - singular with CamelCase
      - *BookClub*
  
  - **Database Table**
    - plural with snake_case
      - *book_clubs*

  - Article - articles
  - LineItem - line_items
  - Deer - deers
  - Mouse - mice
  - Person - people

#### SCHEMA CONVENTIONS

  - Naming conventions used by AR for the *columns in database tables*
  
  - **Foreign keys**
    - should be named following the pattern `singularized_table_name_id`
      - *item_id*, *order_id*
  
  - **Primary keys**
    - integer column named `id`
      - column automatically created

  - *Optional column names*
    - *created_at* - Automatically gets set to the current date and time when the record is first created
    - *updated_at* - Automatically gets set to the current date and time whenever the record is created or updated
    - *lock_version* - Adds optimistic locking to a model.
    - *type* - Specifies that the model uses Single Table Inheritance.
    - *(association_name)_type* - Stores the type for polymorphic associations
    - *(table_name)_count* - Used to cache the number of belonging objects on associations
      - Ex. a comments_count column in an Article class that has many instances of Comment will cache the number of existent comments for each article

### CREATING ACTIVE RECORD MODELS

  - To create AR models, subclass the `ApplicationRecord` class

  ```ruby
  class Product < ApplicationRecord
  end
  ```

  - *Product* model is created, mapped to a *products* table at the database
  - Allows to *map the columns of each row* in that table *with the attributes* of the *instances of the model*

  ```
  CREATE TABLE products (
  id int(11) NOT NULL auto_increment,
  name varchar(255),
  PRIMARY KEY  (id)
  );
  ```
  ```ruby
  p = Product.new
  p.name = "Some Book"
  puts p.name # "Some Book"
  ```

  - Products table created using an SQL
    - two column: id and name
  - Use 

### OVERRIDING THE NAMING CONVENTIONS

  - Can follow a different naming convention and override the default conventions
  - `ApplicationMethod` inherits from `ActiveRecord::Base`
    - `ActiveRecord::Base.table_name=` method to specify the table name to use

  ```ruby
  class Product < ApplicationRecord
    self.table_name = "my_products"
  end
  ```

  - Need to manually define the class name that is hosting the fixtures using `set_fixture_class` method

  ```ruby
  class ProductTest < ActiveSupport::TestCase
    set_fixture_class my_products: Product
    fixtures :my_products
    # ...
  end
  ```

  - Possible to override the column that should be used as the table's primary key using `ActiveRecord::Base.primary_key=` method

  ```ruby
  class Product < ApplicationRecord
    self.primary_key = "product_id"
  end
  ```

### CRUD - READING AND WRITING DATA

  - Create, Read, Update and Delete
  - AR automatically creates methods to allow an application to read and manipulate data stored within its tables

#### CREATE

  - AR objects can be created from a hash, a block or have their attributes manually set after creation
  - `new` method returns a *new object*
  - `create` method returns the *object and save it to the database*

  ```ruby
  user = User.create(name: "David", occupation: "Code Artist")

  user = User.new
  user.name = "David"
  user.occupation = "Code Artist"
  ```

  - Given a model User with attributes name and occupation
    - `create` method create and save a new record into the database
    - `new` instantiates an object without being saved
      - `user.save` will commit the record to the database
  
  ```ruby
  user = User.new do |u|
    u.name = "David"
    u.occupation = "Code Artist"
  end
  ```

  - If a block is provided, both create and new will *yield the new object to that block for initialization*

#### READ

  - *Querying guide* https://edgeguides.rubyonrails.org/active_record_querying.html
  - AR provides a rich API for accessing data within a database

  ```ruby
  # return a collection with all users
  users = User.all

  # return the first user
  user = User.first

  # return the first user named David
  david = User.find_by(name: 'David')

  # find all users named David who are Code Artists
  # sort by created_at in reverse chronological order
  users = User.where(name: 'David', occupation: 'Code Artist').order(created_at: :desc)
  ```

### UPDATE

  - Once the AR object has been retrieved, its *attributes can be modified and saved to the database*

  ```ruby
  user = User.find_by(name: 'David')
  user.name = 'Dave'
  user.save

  # shorthand - use a hash mapping attribute names to the desired value
  #   useful for updating several attributes at once
  user = User.find_by(name: 'David')
  user.update(name: 'Dave')

  # to update several record in bulk - update_all
  #   below two are equivalent
  User.update_all "max_login_attempts = 3, must_change_password = 'true'"
  User.update(:all, max_login_attempts: 3, must_change_password: true)
  ```

#### DELETE

  - Once AR object is retrieved, it can be destroyed which removes it from the database

  ```ruby
  user = User.find_by(name: 'David')
  user.destroy

  # to delete several records in bulk
  #   destroy_by or destroy_all
  User.destroy_by(name: 'David') # find and delete all users named David
  User.destroy_all # delete all users
  ```

### VALIDATIONS

  - *AR validations guide* https://edgeguides.rubyonrails.org/active_record_validations.html
  - AR allows to validate the state of a model prior to writing it into the database
    - Ensure that only valid data is saved into your database
  - *Validations* => attribute value:
    - is not empty
    - is unique
    - not already in the database
    - follows a specific format
    - etc.

  - Validation happens after a fresh object is created/updated (create/update method)
    - AR uses `new_record?` instance method to determine whether an object is already in the database or not

  - Some methods trigger validations, while others do not
    - The following *methods trigger validations*
      - create
      - create!
      - save
      - save!
      - update
      - update!
    - Return false when validation fails and does not perform any operation on the database
      - `save!` and `update!`
        - save and update checks for validation

  ```ruby
  class User < ApplicationRecord
    validates :name, presence: true
  end
    
  irb> Person.create(name: "John Doe").valid?
  => true
  irb> Person.create(name: nil).valid?
  => false
  ```

  - *Custom methods* can be added 

    ```ruby
    class Store < ActiveRecord::Base
      has_many :employees
      validates :name, length: { minimum: 3 }
      validates :annual_revenue, numericality: { greater_than: 0 }
      validate :store_must_carry_apparel

      def store_must_carry_apparel
        if !mens_apparel && !womens_apparel
          errors.add(:base, "Store must carry at least one of the men's or women's apparel")
        end
      end
    end
    ```

### ERRORS

  ```ruby
  puts store.valid?
  # => false
  puts store.errors.any?
  # => true
  puts store.errors.full_messages
  # => "Store must carry at least one of the mens' or women's apparel"
  ```

### MIGRATIONS

  - *AR migrations guide* https://edgeguides.rubyonrails.org/active_record_migrations.html
  - Rails provides a domain-specific language for managing a database schema called migrations
  - Rails keeps track of which files have been committed to the database and provides rollback features
    - To actually create the table, run `bin/rails db:migrate`
    - To roll it back, `bin/rails db:rollback`
    - above code is `database-agnostic:` it will run in MySQL, PostgreSQL, Oracle, and others.
  
  ```ruby
  class CreatePublications < ActiveRecord::Migration[7.1]
    def change
      create_table :publications do |t|
        t.string :title
        t.text :description
        t.references :publication_type
        t.integer :publisher_id
        t.string :publisher_type
        t.boolean :single_issue

        t.timestamps
      end
      add_index :publications, :publication_type_id
    end
  end
  ```

<a id="day2comp"></a>
## **DAY 2 COMPASS NOTES**

### MODEL-VIEW-CONTROLLER (MVC)

![MVC Diagram](https://softcover.s3.amazonaws.com/636/ruby_on_rails_tutorial_6th_edition/images/figures/mvc_schematic.png)

  - Architectural pattern adopted to build modern web applications
  - Standard Rails application structure has `app/` directory
    - Subdirectories:
      - *models*
      - *views*
      - *controllers*
  - *Separation* between the *data* in the application and the *code* used to display it

  - In Rails applcation:
    - A browser sends a *request*
    - Received by a webserver
    - Passed on to a Rails *controller* => in charge of what to do next
      - Immediately render a *view*
      - Interacts with a *model* (more common for dynamic sites)
        - Ruby object that represents an element of the site (i.e. user)
        - In charge of *communicating with database*
    - After invoking the model, the controller then *renders* the view and returns the complete web page to the browser

### MVC IN ACTION

![Detailed MVC Diagram](https://softcover.s3.amazonaws.com/636/ruby_on_rails_tutorial_6th_edition/images/figures/mvc_detailed.png)

  1. The browser issues a request for the /users URL.
  2. Rails routes /users to the index action in the Users controller.
  3. The index action asks the User model to retrieve all users (User.all).
  4. The User model pulls all the users from the database.
  5. The User model returns the list of users to the controller.
  6. The controller captures the users in the @users variable, which is passed to the index view.
  7. The view uses embedded Ruby to render the page as HTML.
  8. The controller passes the HTML back to the browser.4


  - *HTTP request*	*URL*	            *Action*	  *Purpose*
  - GET	            /users	          index	      page to list all users
  - GET	            /users/1	        show	      page to show user with id 1
  - GET	            /users/new	      new	        page to make a new user
  - POST	          /users	          create	    create a new user
  - GET	            /users/1/edit	    edit	      page to edit user with id 1
  - PATCH	          /users/1	        update	    update user with id 1
  - DELETE	        /users/1	        destroy	    delete user with id 1

  - *index / show / new / edit* actions correspond to pages
  - *create / update / destroy* actions to modify information in the database

<a id="day3comp"></a>
## **DAY 3 COMPASS NOTES**

### BUG: MONEY FORMATTING

  - `money-rails` gem
    - https://github.com/RubyMoney/money-rails
  - Include `humanized_money_with_symbol` helpher to show currency with symbol and comma

### UI CHANGE: EMPTY CART

  - **enhanced_cart** variable is inherited from `application_controller.rb`

    - `applcation_controller.rb` is a superclass (i.e. class ApplicationController < ActionController::Base)
      - other controllers are subclasses
        - ex. `class CartsController < ApplicationController`

    - Defined as a method in application controller
      - need `helper_method :enhanced_cart` to be used in the view files
        - can be used without @ symbol in the view file since it is a method that returns @enhanced_cart
        - if it was defined as an instance variable in the cart controller file, would have to use @enhanced_cart in the view file
        ```ruby
        def enhanced_cart
          @enhanced_cart ||= Product.where(id: cart.keys).map {|product| { product:product, quantity: cart[product.id.to_s] } }
        end
        helper_method :enhanced_cart
        ```
  
  - Add bootstrap styling in the view file

### UI CHANGE: ORDER DETAILS

  ```ruby
  <div class="products">
    <%= render @products %>
  </div>
  ```
  - **Rendering @products** will find a partial with the variable's singular name
    - looks for `_product.html.erb`

<a id="day4comp"></a>
## **DAY 4 COMPASS NOTES**

### NAMESPACES

  - A way of bundling logically related objects together
    - Using Modules
    - Allow classes/modules with conflictnig names to co-exist
    - Ex. Different files with the same names but in different folders
  
  ```ruby
  module Perimeter
    class Array
      def initialize
        @size = 400
      end
    end
  end

  our_array = Perimeter::Array.new
  ruby_array = Array.new # Ruby's array class

  p our_array.class   # => Perimeter::Array
  p ruby_array.class  # => Array
  ```

  - Namespaced a new version of array under the Perimeter module

  ```ruby
  module Gym
    class Push
      def up
        40
      end
    end
  end
  require "gym"

  module Dojo
    class Push
      def up
        30
      end
    end
  end
  require "dojo"

  dojo_push = Dojo::Push.new
  p dojo_push.up

  gym_push = Gym::Push.new
  p gym_push.up
  ```
  - When creating libraries with Ruby:
    - A good practice to namespace  code under the name of library or project.

### DATABASE MIGRATION

  - `bin/rake db:migrate` to migrate database
    - does not run if already migrated
  
  - `bin/rails g mirgration add_discuount_cents_to_products`
    - creates a new migration file called `########_add_discuount_cents_to_products.rb`
      - with change method inside
        -  add syntax to modityf table (i.e. add column)
  
  - `bin/rake db:migrate` to run the migration
    - `discount_cents` column added to products table in schema file

  ```ruby
  class AddDiscountCentsToProducts < ActiveRecord::Mirgation
    def change
      add_column :products, :discount_cents, :integer
    end
  end
  ```

  - `bin/rake db:rollback` to *undo migration by one migration*
    - rollbacks schema and undo add_column from above