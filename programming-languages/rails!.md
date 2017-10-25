- https://www.toptal.com/ruby-on-rails
- http://dci-in-ruby.info/technical_overview.html
- https://www.sitepoint.com/dci-the-evolution-of-the-object-oriented-paradigm/
- Complete [Ruby on Rails Tutorial](https://www.railstutorial.org/book)

## Flow of a Rails request
At the highest level, Rails requests are served through an application server, which is responsible for directing an incoming request into a Ruby process. Popular application servers that use the Rack web request interface include Phusion Passenger, Mongrel, Thin, and Unicorn.

Rack parses all request parameters (as well as posted data, CGI parameters, and other potentially useful bits of information) and transforms them into a big Hash (Ruby’s record / dictionary type). This is sometimes called the env hash, as it contains data about the environment of the web request.

In addition to this request parsing, Rack is configurable, allowing for certain requests to be directed to specific Rack apps. If you want, for example, to redirect requests for anything in your admin section to another Rails app, you can do so at the Rack level. You can also declare middleware here, in addition to being able to declare it in Rails.

Those requests that are not directed elsewhere (by you in Rack) are directed to your Rails app where it begins interacting with the Rails ActionDispatcher, which examines the route. Rails apps can be spit into separate Rails Engines, and the router sends the request off to the right engine. (You can also redirect requests to other Rack compatible web frameworks here.)

Once in your app, Rails middleware – or your custom middleware – is executed. The router determines what Rails controller / action method should be called to process the request, instantiates the proper controller object, executes all the filters involved, and finally calls the appropriate the action method.

[Further detail](http://guides.rubyonrails.org/action_controller_overview.html) is available in the Rails documentation.

## The Rails Asset Pipeline
Rails 3.1 introduced the [Asset Pipeline](http://guides.rubyonrails.org/asset_pipeline.html), a way to organize and process front-end assets. It provides an import/require mechanism (to load dependent files) that provides many features. While the Asset Pipeline does have its rough edges, it does solve and provide many of the modern best practices in serving these files under HTTP 1.1. Most significantly, the Asset Pipeline will:

Collect, concatenate, and minify all assets of each type into one big file
Version files using fingerprinting to bust old versions of the file in browser caches
The Asset Pipeline automatically brings with it Rails’ selection of Coffeescript as its JavaScript pre-processed / transpiled language of choice and SASS as its CSS transpiled language. However, being an extensible framework, it does allow for additional transpiled languages or additional file sources. For example, [Rails Assets](https://rails-assets.org/#/) brings the power of Bower to your Rails apps, allowing you to manage third-party JavaScript and CSS assets very easily.

## ActiveRecord
[Active Record](http://guides.rubyonrails.org/active_record_basics.html) was described by Martin Fowler in his book Patterns of Enterprise Application Architecture as “an object that wraps a row in a database table or view, encapsulates the database access, and adds domain logic on that data”.

ActiveRecord is both an Object Relational Mapping (ORM) design pattern, and Rails’ implementation of that design pattern. This means that fetching, querying, and storing your objects in the database is as much a part of the API of your objects as your custom business logic. A developer may see this as an undesired side effect, or as a welcome convention, depending on their preference and level of experience.

## Arel
[Arel](https://github.com/rails/arel) provides a query API for ActiveRecord, allowing Rails developers to perform database queries without having to hand-write SQL. Arel creates lazily-executed SQL whereby Rails waits until the last possible second to send the SQL to the server for execution. This allows you to take an Arel query and add another SQL condition or sort to the query, right up to the point where Rails actually executes the query. Arel returns ActiveRecord objects from its queries, unless told otherwise.

## Convention over Configuration pattern
Convention over Configuration (CoC) is a software design pattern by which only the unconventional aspects of an application need to be specified by a developer. When the default convention matches the desired behavior, the default behavior is followed without any configuration being required. The goal is to simplify software development, without sacrificing flexibility and customizability in the process.

Here are some examples of how CoC principles are applied in Rails:
* Model and database table naming. Rails automatically pluralizes class names to find the respective database tables. For a class Book, for example, it will expect a database table named books. For class names composed of multiple words, the model class name should employ CamelCase (e.g., BookClub and book_clubs).
Primary and foreign keys. By default, Rails uses an integer column named id as the table’s primary key. Foreign key names by default follow the pattern of appending _id to the singularized tablename (e.g., item_id for a foreign key into the items table).
Reserved words for automatic functionality. There are also some optional column names which, if used, automatically add features and functionality to Rails database tables. created_at, for example, will automatically be set to the date and time when the record was created. Similarly, updated_at will automatically be set to the date and time whenever the record was last updated.
Auto-loading of class definitions. Auto-loading is the “magic” by which classes appear to be accessible from anywhere, without the need to explicitly require them. Here’s how it works: When you reference a class in your code, Rails takes the class name (with namespace) as a string, calls underscore on it, and looks for a file with that name (in all directories specified in your config.autoload_paths). For example, if you reference a class named FileHandling::ZipHandler, Rails will automatically search for file_handling/zip_handler.rb in your config.autoload_paths. This feature often results in novice Rails programmers thinking that they don’t need to explicitly require referenced classes and that Rails will just auto-magically find them anyway. They then become baffled when they don’t follow this convention and are suddenly being told by Rails that their classes can’t be found.
It is important to note that CoC specifies a default –- but not immutable –- convention. Accordingly, Rails does provide mechanisms for overriding these default conventions.
