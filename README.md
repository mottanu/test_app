# test_app

A small Rails storefront / portfolio site. Static pages (stores, about,
contact, tasche) are served by `PagesController`; `products` and `creatives`
are scaffolded CRUD resources. The root route is `pages#stores`.

## Stack

- Ruby 2.0.0 (pinned in the `Gemfile`)
- Rails 4.1.6
- SQLite3 in development and test; PostgreSQL (`pg`) + Unicorn in production
- Sass, CoffeeScript, jQuery, Turbolinks, Jbuilder
- Targets Heroku (`rails_12factor`, `config/unicorn.rb`)

## Running locally

```
# Ruby 2.0.0 required, e.g. via rbenv or rvm
gem install bundler
bundle install --without production
bundle exec rake db:migrate
bundle exec rails server
```

Then open http://localhost:3000.

## Tests

```
bundle exec rake db:test:prepare
bundle exec rake test
```

Tests are the default Rails Minitest suite under `test/`.

## Known issues

- `config/secrets.yml` is committed to git. Rotate the secret and move it to
  an environment variable (e.g. `ENV["SECRET_KEY_BASE"]`).
- `.DS_Store` files are tracked in many directories; remove them and add
  `.DS_Store` to `.gitignore`.
- The Heroku Procfile was saved as `app/Procfile.rtf`. It needs to be a plain
  text `Procfile` in the project root.
- `rails_log_stdout` and `rails3_serve_static_assets` are pulled from GitHub
  (`heroku/...`). They are obsolete; `rails_12factor` already covers both.
- `app/views/pages/creatives.html.erb` exists but there is no
  `get 'pages/creatives'` route (only `resources :creatives`, which has no
  views), so the page is unreachable.
