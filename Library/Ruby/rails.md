# RUBY

  - Rails is a *web application development framework* written in the Ruby language
  - **Rails Philosophy** - Two major guiding principles
    1. Don't Repeat Yourself (DRY)
    2. Convention Over Configuration

  - Rails comes with a number of scripts called *generators*
    - Designed to make development easier by creating everything that's necessary to start working
  - `new` generator
    - Provide the foundation of a fresh Rails application
    - `rails new blog`

## CONTROLLER

  - Plce where all of the *route logic* exists
  - To *receive specific requests* for the application
  - *Routing* decides which controller receives which requests
    - Often more than one route to each controller
    - Different routes can be *served by different actions*
      - Each action's purpose is to *collect information* to provide it to a *view*
        - View's purpose is to *display information* in a human readable format
        - *Controller* collects information
        - *View* just displays
          - View templates written in a language called *eRuby* (Embedded Ruby)

### CREATING A NEW CONTROLLER

  - `bin/rails generate controller welcome index`
    - *controller* gnerator
    - *welcome* controller
    - *index* action

  - Create a bunch of files for welcome including controller and view
    - *app/controllers/welcome_controller.rb*
      - with class name of WelcomeController
      - inside the class, *define methods* that will be come the *actions for this controller*
        - actions will perform CRUD operations
        - only public methods can be actions for controllers
    - *app/views/welcome/index.html.erb*

### SETTING THE APPLICATION HOME PAGE

  - `config/routes.rb` is the application's routing file
    - Tells Rails how to connect incoming requests to controllers and actions

  - To *connect the root* of the site to a specific controller and action
    - `root 'welcome#index'`
      - *Map requests to the root* of the application to the *welcome controller's index action*
    - `get welcome/index`
      - Map requests to *http://localhost:3000/welcome/index*

    ```ruby
    Rails.application.routes.draw do
    root 'welcome#index'
    end
    ```

## GETTING UP AND RUNNING

  - *Resource* is a collection of similar objects
    - Ex. articles, people, animals, etc.
  - CRUD operations to CRUD items for a resource

### RESOURCES METHOD

  - `resources` method can be used to *declare a standard REST resource*
    - `bin/rake routes` list the defined routes and all the standard RESTful actions

    ```ruby
    Rails.application.routes.draw do
      resources :articles
    
      root 'welcome#index'
    end

    # bin/rake routes
          Prefix Verb   URI Pattern                   Controller#Action
        articles GET    /articles(.:format)           articles#index
                 POST    /articles(.:format)          articles#create
    new_article  GET     /articles/new(.:format)      articles#new
    edit_article GET    /articles/:id/edit(.:format)  articles#edit
         article GET     /articles/:id(.:format)      articles#show
                 PATCH   /articles/:id(.:format)      articles#update
                 PUT     /articles/:id(.:format)      articles#update
                 DELETE  /articles/:id(.:format)      articles#destroy
            root GET    /                             welcome#index
    ```

## CREATE

  - After including the resources method in the routes file, the routes are not created yet
  - Routes need to have a *controller* defined in order to *serve the request*
    - `bin/rails generate controller articles`
  - *Actions (method)* need to be defined *inside the controller*
  - *Views* associated with actions need to be created 
    - Without views, error:
      - `Missing template articles/new, application/new with {locale:[:en], formats:[:html], handlers:[:erb, :builder, :coffee]}. Searched in: * "/path/to/blog/app/views`
        - missing template in app/views directory
        - in {}, indicates what kind of template is needed
          - *formats* and *handlers* (i.e. extension => .html.erb)
    
    ```ruby
    # app/controllers/articles_controller.rb
    class ArticlesController < ApplicationController
      # action (method)
      def new
      end
    end

    # app/views/new.html.erb
    <h1>New Article</h1>
    ```

### CREATE FORM

  - `form_for` helper method
    - pass an identifying object for this form => `:article`
    - `f` FormBuilder object is used to build the form
    - by default, *action attribute* for the form points at /articles/new (i.e. form page)
      - resolve by including `:url articles_path` helper
        - tells Rails to point the form to the URI Pattern associated with the articles prefix (bin/rake routes)
        - sends POST request to that route (i.e. *create* action for form)

    ```erb
    <%= form_for :article, url: articles_path do |f| %>
      <p>
        <%= f.label :title %><br>
        <%= f.text_field :title %>
      </p>

      <p>
        <%= f.label :text %><br>
        <%= f.text_area :text %>
      </p>

      <p>
        <%= f.submit %>
      </p>
    <% end %>
    ```

  - *create* action needs to be created within the ArticlesController class
    - when form is submitted, the *fileds of the form* are sent to Rails as *parameters*
      - parameters can be referenced inside the controller actons
      - to print parameters: `render plain: params[:article].inspect`
        - key of *plain*
        - value of *params[:article].inspect*
        - *params* method is the object which represents the parameters (or fileds) from the form
        - result of render: `{"title"=>"First article!", "text"=>"This is my first article."}`
      - URL: http://www.example.com/?username=dhh&email=dhh@email.com
        - params[:username] would equal "dhh"
        - params[:email] would equal "dhh@email.com"

#### CREATING MODEL

  - Generator used to *create models*
    - `bin/rails generate model Article title:string text:text`
      - *Article* model
      - title *attribute* of *type* string
      - text *attribute* of *type* text
    - Attributes are automatically added to the *articles table* in the database
      - *Mapped* to Article model
    - Creates a bunch of files including model and database
      - *app/models/article.rb*
      - *db/migrate/20140120191729_create_articles.rb*
        - responsible for creating the database structure (database migration file)
        - AR automatically map *column names to model attributes*
          - no need to declare attributes inside Rails models

#### RUNNING MIGRATION

  - `bin/rake db:migrate` rake command to run the migration
    - tables created
    - method inside the migration file will be called

#### SAVING DATA IN CONTROLLER

  - Grabbing and automatically assgining all controller parameters to the model in on shot makes it easier
    - However, allows malicious use
  - *Whitelist controller parameters* to prevent wrongful mass assignment
    - Both allow and require the title and text parameters for valid use of create
      - *require* and *permit*
    - Often *factored out into its own method (i.e. private method)*
      - Reused by multiple actions
        - Ex. create and update

  ```ruby
  class ArticlesController < ApplicationController
    def new
    end

    def create
      # mass assignment - not safe
      # @article = Article.new(params[:article])

      # whitelist controller parameters - safe
      # @article = Article.new(params.require(:article).permit(:title, :text))

      @article = Article.new(aticle_params)

      @article.save
      redirect_to @article
    end

    private
    def article_params
      params.require(:article).permit(:title, :text)
    end
  end
  ```

### READ

#### SHOWING

  - `article GET    /articles/:id(.:format)      articles#show`
    - `:id` tell that this route expects an :id parameter
      - id of the article

  - Good practice to *place the standard CRUD actions* in each controller in the following order:
    - *index*
    - *show*
    - *new*
    - *edit*
    - *create*
    - *update*
    - *destroy*

    ```ruby
    # controller.rb
    class ArticlesController < ApplicationController
      def show
        @article = Article.find(params[:id])
      end
    
      def new
      end
    end

    # show.html.erb
    <p>
      <strong>Title:</strong>
      <%= @article.title %>
    </p>
    
    <p>
      <strong>Text:</strong>
      <%= @article.text %>
    </p>
    ```

### LISTING ALL

  - `articles GET    /articles(.:format)          articles#index`

    ```ruby
    # controller.rb
    class ArticlesController < ApplicationController
      def index
        @articles = Article.all
      end

      def show
        @article = Article.find(params[:id])
      end
    
      def new
      end
    end

    # show.html.erb
    <h1>Listing articles</h1>
    
    <table>
      <tr>
        <th>Title</th>
        <th>Text</th>
      </tr>
    
      <% @articles.each do |article| %>
        <tr>
          <td><%= article.title %></td>
          <td><%= article.text %></td>
        </tr>
      <% end %>
    </table>
    ```

### ADDING LINKS

  - `link_to` built-in view helper method to *create hyperlinks*
  - To link to an action in the *same controller*, *no `controller:`*

    ```erb
    <%= link_to 'My Blog', controller: 'articles' %> 
    <%= link_to 'New article', new_article_path %>
    <%= link_to 'Back', articles_path %>
    <%= link_to 'Back', articles_path %>
    ```

### ADDING VALIDATIONS

  ```ruby
  def new
    @article = Article.new
  end
  
  def create
    @article = Article.new(article_params)
  
    if @article.save
      redirect_to @article
    else
      render 'new'
    end
  end
  
  private
    def article_params
      params.require(:article).permit(:title, :text)
    end
  ```

  - When @article.save return false, `render` is used instead of redirect
    - So that the *@article object is passed back* to the new template when it is rendered
    - Rendering is *done with the same request as the form submission*
      - whereas the redirect_to tells the browser to issue another request
  
  ```erb
  # display error
  <%= form_for :article, url: articles_path do |f| %>
  
    <% if @article.errors.any? %>
      <div id="error_explanation">
        <h2>
          <%= pluralize(@article.errors.count, "error") %> prohibited
          this article from being saved:
        </h2>
        <ul>
          <% @article.errors.full_messages.each do |msg| %>
            <li><%= msg %></li>
          <% end %>
        </ul>
      </div>
    <% end %>
  
    <p>
      <%= f.label :title %><br>
      <%= f.text_field :title %>
    </p>
  
    <p>
      <%= f.label :text %><br>
      <%= f.text_area :text %>
    </p>
  
    <p>
      <%= f.submit %>
    </p>
  
  <% end %>
  
  <%= link_to 'Back', articles_path %>
  ```

  - Added `@article = Article.new` in the controller 
    - Otherwise, @article would be *nil* in the view
  - Fields that contain errors are wrapped with a div with class `field_with_errors`
    - title wrapped with a div with the class

## UPDATE

  ```ruby
  # edit.html.erb
  <%= form_for :article, url:article_path(@article), method: :patch do |f| %>

  #controller.rb
    def edit
      @article = Article.find(params[:id])
    end

    def update
      @article = Article.find(params[:id])

      if @article.update(article_params)
        redirect_to @article
      else
        render 'edit'
      end
    end
  ```

  - `method: :patch` to submit form via the *PATCH HTTP method*
  - `@article.update()` do not need to be passed in all attributes for update
    - `@article.update(params.require(:article).permit(:title))` would only update the title attribute

## PARTIALS

  - Using partials, repeated code can be extracted
    - Partial files are prefixed with underscore
      - Ex. `_form.html.erb`

  ```erb
  <%= form_for @article do |f| %>
  # ...
  <% end %>
  ```

  - `@article` is a resource corresponding to a full set of RESTful routes
    - No need to define url, method, etc. (*resource-oriented style*)
      - <%= form_for :article, url:article_path(@article), method: :patch do |f| %>
      - <%= form_for :article, url: articles_path do |f| %>
      - https://api.rubyonrails.org/classes/ActionView/Helpers/FormHelper.html#method-i-form_for-label-Resource-oriented+style
    - Defined in routes file `resources :articles`

## DELETE

  - `DELETE /articles/:id(.:format)      articles#destroy`
    - `destroy` method in the controller

  ```ruby
  # controller.rb
  def destroy
    @article = Article.find(params[:id])
    @article.destroy

    redirect_to articles_path
  end

  # index.html.erb
  <td><%= link_to 'Delete', article_path(article),
        method: :delete,
        data: { confirm: 'Are you sure?' } %>
  </td>
  ```

  - `:method` and `data` options (HTML5 attributes) passed in for delete link
    - First show confirm dialog and submit the link with delete method
    - Done via JavaScript file jquery_ujs
      - Automaticlly included into application's layout 
        - app/views/layouts/application.html.erb

## SECOND MODEL

### ASSOCIATING MODELS

  - `belongs_to` and `has_many`syntax to declare the relationship between models
    - One article can have many comments
    - Each comment belongs to one article
    - `dependent: :destroy` to delete all the comments when article is deleted
  - From instance variable @article containing an article
    - All the comments belonging to that article can be *retrieved* as an *array* using `@article.comments`

  ```ruby
  class Article < ActiveRecord::Base
    has_many :comments, dependent: :destroy
    validates :title, presence: true,
                      length: { minimum: 5 }
  end

  class Comment < ActiveRecord::Base
    belongs_to :article
  end
  ```

### ADDING A ROUTE FOR SECOND MODEL

  - To add a route so that Rails knows where to navigate to see comments
    - Comments as a *nested resource* within articles

  ```ruby
  resources :articles do
    resources :comments
  end
  ```

### GENERATING A CONTROLLER FOR SECOND MODEL

  - Include a form for comments in Article show template

  ```ruby
  # comments_controller.rb
  class CommentsController < ApplicationController
    def create
      @article = Article.find(params[:article_id])
      @comment = @article.comments.create(comment_params)
      redirect_to article_path(@article)
    end
  
    private
      def comment_params
        params.require(:comment).permit(:commenter, :body)
      end
  end
  ```

  - Each request for a comment has to keep track of the article to which the comment is attached
    - Initial call to the find method of the Article model
  - `@article.comments` to automatically link the comment to particular article

## SECURITY

### BASIC AUTHENTIFICATION

  - `http_basic_authenticate_with` method allows access to the requested action if that method allows it
    - At the top of the controller file
  - Asks for authentification except index and show methods for article and only for destroy method for comments
  ```ruby
  # articles_controller.rb
  http_basic_authenticate_with name: "dhh", password: "secret", except: [:index, :show]

  # comments_controller.rb
  http_basic_authenticate_with name: "dhh", password: "secret", only: :destroy
  ```