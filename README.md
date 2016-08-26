
This is the [Github Pages](http://pages.github.com/) source code for the [Socrata Datasync Documentation Page](http://socrata.github.io/datasync/ (currently deployed to <http://socrata.github.io/datasync/>.

## Contributing

We love pull requests! If you'd like to contribute, feel free to send us pull requests.

### Setting Up

The site is a customized [Jekyll](http://jekyllrb.com/) site, so there are some steps you'll need to take care of to get your environment set up:

1. Make sure you have the `gh-pages` branch checked out: `git checkout -b gh-pages origin/gh-pages`
2. Pull in the site templates and CSS/SASS, which come from submodules: `git submodule update --init`
3. Make sure you have Ruby version installed. Check `.ruby-version` to see the preferred version. If you're using rbenv or rvm, this should automatically be set up gh-pahes is still in ruby 2.1.7 so use rvm to switch to that ruby version
4. Install the Bundler Gem installed: `gem install bundler && bundle`
5. Make sure you have the `jekyll` RubyGem installed
6. jekyll serve to serve your local version and make sure you're running at http://0.0.0.0:4000/datasync/

### Modifying CSS/SASS

Site styling is controlled via `css/local.sass` and it's automatically regenerated by Github Pages with each push.