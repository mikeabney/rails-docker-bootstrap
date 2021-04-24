# Rails Docker Bootstrap

Spin up a basic Rails app with the included Docker setup and script. This allows
for creating a new app without installing Ruby or Rails separately on the local
host. That means no fiddling with rvm, rbenv, asdf or whatever else. An article
that goes into just a bit of detail around the whys and hows of this coming into
existence is available here:
[Bootstrap Rails Development with Docker](https://mikeabney.dev/articles/2021-04/rails-docker-bootstrap/)

## Usage

The `dev` script is used to run a set of commands that will auto-generate most
of what is needed to get a Rails app off the ground. The available commands are:

* `new` creates a default Gemfile that pulls the latest Rails version and runs
  `rails new`. This will take a while as it pulls all the needed dependencies,
  including gems, node packages, etc. It will not run if there is already a
  Gemfile in place.
* `setup` runs Rails setup to initialize databases for dev and test, once
  configured (see below).
* `bash` to get a prompt for running `bundle install`, `irb`, the Rails console,
  etc.
* `test` set to run `rspec` tests once set up (see below).
* `up` which is a little better than simple `docker-compose up` because it
  cleans up the app container after it's done.
* `down` basically an alias for `docker-compose down`.
* `build` builds or rebuilds the image. Only needed if ther are changes to
  `Dockerfile.dev` or `docker-compose.yml`.

### Step by step

1. Download (probably not clone or fork, but your choice) this repo to a
   directory named for the app you are building.
1. Review what the script and Docker files do. (Don't trust random scripts on
   the internet, kids!)
1. Run `./dev new` and go get some tea, take a bio break, or anything to waste
   a few minutes while images are build, the gems and node packages are
   downloaded, etc.
1. Edit the `database.yml` appropriately (look at the `docker-compose.yml` for
   creds, hostname, etc). Also, consider doing better with password hygiene if
   you ever push the actual Rails app somewhere public.
1. Run `./dev setup`.
1. Test out the app by running `./dev up` and going to `localhost:3000`.

### Notes

The script and compose file are set to spin up a PostgreSQL database.
This is what I use most often. It should be relatively simple to change as you
like.

If you want the `./dev test` command to work, you'll need to set up RSpec in the
usual ways.
