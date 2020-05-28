# SaySo Backend: Rails

## Overview

A functioning hobby project to bring my Ruby and Rails skills up to date. The is the Microservice half of a single-page blogging platform.

This project has:

* **MicroService API** - Backed by SQLite. Functions:
  * **Login**
  * **Logout**
  * **Signup**
  * **User Profile CRUD**
  * **Post CRUD**
  * **Comments CRUD**

[Frontend is in this repo](https://github.com/iq9/say-so-frontend-vanilla).

## Technologies

* **Ruby 2 on Rails 5**
* **SQLite**
* **JWT Auth** - For authentication between front and back.

## Setup

- Clone this repo
- `bundle install` - Install Dependencies
- `rake schema:load` - Load the Schema. Although it should already by there. It's in the SQLite file.
- `rake seed` - Not necessary.
- `rails s` - Start the server

* Service should now be browseable at: http://localhost:3000/

Service must be running for the Frontend app to work. It makes an REST calls to it.

## Tools

* **MacOS**
* **[VS Code](https://code.visualstudio.com/)**
* **[Table Plus](https://tableplus.com/)**

## Screenshots

coming

## Libraries

- [acts_as_follower](https://github.com/tcocca/acts_as_follower) - Adds Followers functionality
- [acts_as_taggable](https://github.com/mbleigh/acts-as-taggable-on) - Adds Tagging functionality
- [Devise](https://github.com/plataformatec/devise) - Auth and RBAC
- [Jbuilder](https://github.com/rails/jbuilder) - JSON rendering gem. Allows reusable JSON templates.
- [JWT](https://github.com/jwt/ruby-jwt) - JWT security

## Configuration

### camelCase Payloads

- [`config/initializers/jbuilder.rb`](https://github.com/gothinkster/rails-realworld-example-app/blob/master/config/initializers/jbuilder.rb) - Jbuilder configuration for camelCase output
- [`app/controllers/application_controller.rb#underscore_params!`](https://github.com/gothinkster/rails-realworld-example-app/blob/master/app/controllers/application_controller.rb#L44) - Convert camelCase params into snake_case params

### null_session

Prefvents Rails trowing errors when no CSRF token is passed. We use JWT's to authenticate instead of sessions. We specify `:null_session` in [app/controllers/application_controller.rb](https://github.com/gothinkster/rails-realworld-example-app/blob/master/app/controllers/application_controller.rb#L4).

### Authentication

Requests require an `Authorization` HTTP header with a valid JWT. The [application_controller.rb#authenticate_user!](https://github.com/gothinkster/rails-realworld-example-app/blob/master/app/controllers/application_controller.rb#L32) filter is used like the one provided by Devise,. It will respond with a 401 if the request requires Authentication but doesn't get it. The [application_controller.rb#authenticate_user](https://github.com/gothinkster/rails-realworld-example-app/blob/master/app/controllers/application_controller.rb#L18) filter is called on every request to try and authenticate the `Authorization` header. It will only interrupt the request if a JWT is present and invalid. User ID is parsed from the JWT and stored in an instance var called [`@current_user_id`](https://github.com/gothinkster/rails-realworld-example-app/blob/master/app/controllers/application_controller.rb#L24). `@current_user_id` can be accessed in any controller to save a trip to the DB. Otherwise, we can call [`current_user`](https://github.com/gothinkster/rails-realworld-example-app/blob/master/app/controllers/application_controller.rb#L36) to fetch the authenticated user from the DB.

Devise only requires an Email and Password upon registration. To allow additional parameters on sign up, we use [application_controller#configure_permitted_parameters](https://github.com/gothinkster/rails-realworld-example-app/blob/master/app/controllers/application_controller.rb#L14) to allow additional parameters.
