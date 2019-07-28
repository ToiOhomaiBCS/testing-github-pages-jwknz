# Install the software

* Ruby Devkit
* Nodejs (already on Lab machine)
* Git (already on Lab machine)

# Create Project

Setup a new project by doing the folliwing:

replace the `my-awesome-site` with the name of your project

```
~ $ gem install bundler jekyll
~ $ jekyll new my-awesome-site
~ $ cd my-awesome-site
```

You can run the basic website by typing in `bundle exec jekyll serve` in your terminal.

You can stop the server at anytime by typing in `Ctrl+C`

# Adding a git repository

Add a git repository by typing in: `git init` in your terminal.

Add the remote connection by typing in:

```
git remote add origin your-supplied-url
```

You will be given a URL for your assignment, but you can create a repository and use that instead.

Just note that you will need to put the name of your repository in the `baseurl:` parameter of the `_config-prod.yml` file that you will create below.

Once you have done these steps it pays to do a commit and a push to make sure everything is setup correctly.

# Github Pages theme

Select the theme of what you want your website to look like from here:

[https://pages.github.com/themes/](https://pages.github.com/themes/)

# Scripts (copy and paste)

## Setting up package.json

```
npm init -y
```

Replace the script object with this:

```
"scripts": {
    "clean": "rm -rf Gemfile.lock .bundle vendor node_modules .sass-cache _site",
    "commit": "git add . && git commit -m \"deploy it\" && git push origin master",
    "gh-pages": "gh-pages -d _site",
    "build": "bundle exec jekyll build --config _config-prod.yml",
    "start" : "bundle exec jekyll build --config _config.yml && live-server --no-browser --port=5500 _site",
    "deploy": "npm run build && npm run commit && npm run gh-pages"
}
```

Add the following at the bottom, before the last closing tag

```
"dependencies": {
    "gh-pages": "^2.0.1",
    "live-server": "^1.2.1"
}
```

## Setting up _config.yml

Replace the contents of your **_config.yml** with the following:

```
title: Your awesome title
email: your-email@example.com
description: >- # this means to ignore newlines until "baseurl:"
  Write an awesome description for your new site here. You can edit this
  line in _config.yml. It will appear in your document head meta (for
  Google search results) and in your feed.xml site description.
baseurl: "" # the subpath of your site, e.g. /blog
twitter_username: jekyllrb
github_username:  jekyll

relative_links:
  enabled:     true
  collections: false

markdown: kramdown
theme: minima
plugins:
  - jekyll-feed
```

## Setting up _config-prod.yml

Create a new file and call it `_config-prod.yml`

The only difference is the baseurl value, but it has to be a separate file.

```
title: Your awesome title
email: your-email@example.com
description: >- # this means to ignore newlines until "baseurl:"
  Write an awesome description for your new site here. You can edit this
  line in _config.yml. It will appear in your document head meta (for
  Google search results) and in your feed.xml site description.
baseurl: "/testing-github-pages-jwknz" # the subpath of your site, e.g. /blog
twitter_username: jekyllrb
github_username:  jekyll

relative_links:
  enabled:     true
  collections: false

markdown: kramdown
theme: minima
plugins:
  - jekyll-feed

```

# Setting up your Gemfile

THe Gemfile has been created, but replace all of the content with the following.

```
source "https://rubygems.org"
gem "github-pages"
gem "minima"
```

# Setting up a gitignore file

Create a **.gitignore** file and add the following.

```
_site
.sass-cache
.jekyll-metadata
vendor
.sass-cache
node_modules
```