Heroku Ruby Jekyll Buildpack
============================

Heroku Ruby Jekyll Buildpack is a fork of Heroku's [official Ruby buildpack](https://github.com/heroku/heroku-buildpack-ruby) with added support for generating static [Jekyll](https://github.com/mojombo/jekyll) sites during the build/deployment stage.

With this [buildpack](http://devcenter.heroku.com/articles/buildpacks) you no longer need pre-build the site or commit the _site build directory to your repo. This simplifies the deployment process and keeps the repo clean. All of the standard Ruby tools are maintained in this buildpack, so you can take full advantage of Rack middleware and other useful tools from the Ruby ecosystem.


## Usage
    $ heroku create --buildpack heroku/ruby

    heroku create --buildpack http://github.com/mattmanning/heroku-buildpack-ruby-jekyll.git

or add this buildpack to your current app

    heroku config:add BUILDPACK_URL=http://github.com/mattmanning/heroku-buildpack-ruby-jekyll.git

Create a Ruby web app with dependencies managed by [Bundler](http://gembundler.com/) and a Jekyll site. [Heroku-Jekyll-Hello-World](https://github.com/burkemw3/Heroku-Jekyll-Hello-World) can be used as a sample starter.

    git push heroku master

Watch it "Building jekyll site"

    -----> Fetching custom git buildpack... done
    -----> Ruby/Rack app detected
    -----> Installing dependencies using Bundler version 1.3.0.pre.5
           Running: bundle install --without development:test --path vendor/bundle --binstubs vendor/bundle/bin --deployment
           Using posix-spawn (0.3.6)
           Using albino (1.3.3)
           Using fast-stemmer (1.0.0)
           Using classifier (1.3.3)
           Using daemons (1.1.4)
           Using directory_watcher (1.4.1)
           Using eventmachine (0.12.10)
           Using kramdown (0.13.3)
           Using liquid (2.3.0)
           Using syntax (1.0.0)
           Using maruku (0.6.0)
           Using jekyll (0.11.0)
           Using rack (1.3.5)
           Using rack-contrib (1.1.0)
           Using rack-rewrite (1.2.1)
           Using thin (1.3.1)
           Using bundler (1.3.0.pre.5)
           Your bundle is complete! It was installed into ./vendor/bundle
           Cleaning up the bundler cache.
           Would have removed bundler (1.2.1)
           Building jekyll site
           Configuration from /tmp/build_2khwpm40t8wev/_config.yml
           Building site: . -> ./_site
           Successfully generated site: . -> ./_site
    -----> Discovering process types
           Procfile declares types     -> web
           Default types for Ruby/Rack -> console, rake

    -----> Compiled slug size: 6.1MB
    -----> Launching... done, v99
    -----> Deploy hooks scheduled, check output in your logs
           http://mattmanning.herokuapp.com deployed to Heroku

See Also
--------

The blog post introducing this buildpack: [http://mwmanning.com/2011/11/29/Run-Your-Jekyll-Site-On-Heroku.html](http://mwmanning.com/2011/11/29/Run-Your-Jekyll-Site-On-Heroku.html).
           Procfile declares types -> (none)
           Default types for Ruby  -> console, rake

The buildpack will detect your app as Ruby if it has a `Gemfile` and `Gemfile.lock` files in the root directory. It will then proceed to run `bundle install` after setting up the appropriate environment for [ruby](http://ruby-lang.org) and [Bundler](https://bundler.io).

## Documentation

For more information about using Ruby and buildpacks on Heroku, see these Dev Center articles:

- [Heroku Ruby Support](https://devcenter.heroku.com/articles/ruby-support)
- [Getting Started with Ruby on Heroku](https://devcenter.heroku.com/articles/getting-started-with-ruby)
- [Getting Started with Rails 4 on Heroku](https://devcenter.heroku.com/articles/getting-started-with-rails4)
- [Buildpacks](https://devcenter.heroku.com/articles/buildpacks)
- [Buildpack API](https://devcenter.heroku.com/articles/buildpack-api)

## Hacking

To use this buildpack, fork it on Github.  Push up changes to your fork, then create a test app with `--buildpack <your-github-url>` and push to it.

### Testing

The tests on this buildpack are written in Rspec to allow the use of
`focused: true`. Parallelization of testing is provided by
https://github.com/grosser/parallel_tests this lib spins up an arbitrary
number of processes and running a different test file in each process,
it does not parallelize tests within a test file. To run the tests: clone the repo, then `bundle install` then clone the test fixtures by running:

```sh
$ bundle exec hatchet install
```

```sh
$ bundle exec rake spec
```
