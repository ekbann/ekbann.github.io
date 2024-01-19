---
layout: post
title:  "Blogging with Jekyll and MathJax"
date:   2024-01-18 15:00:00 -0300
categories: github jekyll mathjax blog
---
### A simple blog using GitHub, Jekyll and MathJax

![Jekyll-MathJax logo](/assets/img/jekyll-mathjax.png "Jekyll-MathJax logo")

There are several ways to create your personal blog on the web, but not as many alternatives when you want to focus on technical subjects and want to write mathematical equations. In this brief article, I explain how you can use GitHub with Jekyll to create your personal blog with MathJax, so you can write beautiful equations using Latex notation. Note that this tutorial is written for Ubuntu, but can easily be adapted for a different OS.

## What is Jekyll and MathJax

In this tutorial, I will assume that you now what GitHub is, and that you can use it to host your personal website using GitHub Page. If you don’t, then take a look at this Tutorial. With that being said, let’s explain what Jekyll and MathJax are…

>Jekyll is a static site generator. It takes text written in your favorite markup language and uses layouts to create a static website. You can tweak the site’s look and feel, URLs, the data displayed on the page, and more.
>
>— Jekyll Official Website

In other words, Jekyll can be thought as an application written in Ruby, that easily creates a web site that is easily manageable and allows one to write using markup language, which is quite handy. Also, Jekyll is supported by Github and has some pre-built styles, so your blog is beautiful looking right out of the box.

>MathJax is a JavaScript display engine for mathematics that works in all browsers.
>
>— MathJax Official Website

In other words, MathJax is a service that renders the mathematical equation, so it looks neat in your browser. You can then write in your blog `$$ E = mc^2 $$` and in your browser, MathJax will render it as:

$$ E = mc^2 $$

The idea is to create a GitHub page, then to use Jekyll to style your blog and allow the use of markdown, together with MathJax to properly render the equations.

## Setting up your Blog with Jekyll

There are several ways to set up Jekyll with your GitHub page. One can install themes using Ruby Gems, or use one of the themes provided by GitHub. But to enable MathJax, one has to manually tweak the html code for the theme. So instead, we will fork an specific theme, and modify it.

First, we need to install Jekyll and Bundle (which helps manage Ruby Gems). If you are using Ubuntu 20.04, you might already have Ruby installed (check with `ruby -v` and `gem -v`). Otherwise, you might need to install it. The command below will install Ruby.

```
sudo apt install ruby-full
```

To install *RubyGems*, we need development packages installed. Some distributions already has this installed. Check with `gcc -v`,`g++ -v`, and `make -v`. If they are missing, install them with:

```
sudo apt install build-essential zlib1g-dev
```

Avoid installing RubyGems packages (called gems) as the root user. Instead, set up a gem installation directory for your user account. The following commands will add environment variables to your `~/.bashrc` file to configure the gem installation path:

```
echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

Finally, install Jekyll and Bundler:

```
gem install jekyll bundler
```

If you get *permission errors* like I did running inside Crostini on a Chromebook, run instead:

```
sudo gem install jekyll bundler
```

Sometimes you will need to satisfy a few dependencies. Do so with:

```
sudo bundle install
```

That’s it! You’re ready to start using Jekyll. Now you can set up your blog with Jekyll, executing:

```
jekyll new my-website
```

This will create a folder “my-website” with all website code inside it. If you go inside the directory and run one command, you can start a local server with your blog running.

```
cd ./my-website
bundle exec jekyll serve
```

Now go into your browser and go to “localhost:4000” and you can see your blog.

Your blog is already functional! You can just copy all the files inside the “./my-website” folder, and move them to your git repository (make sure the repository is called *your_github_username*.github.io and that it is completely empty), and then push them to GitHub. After a few seconds, your blog will be up on the web. Below I show an example using a fictitious username called *blogger*:

```
git clone https://github.com/blogger/blogger.github.io
mv ./my-website/* ./blogger.github.io
cd ./blogger.github.io
git add .
git commit -m “Initiated my Jekyll blog”
git push
```

## Quick guide to using Jekyll

Now, I’ve explained how to set up Jekyll, but not exactly how to use it. There is a ton of tutorials out there, but, actually, you don’t need to know much to start using Jekyll effectively. Once your blog is created, to personalize it and start writing posts is straightforward. If you go inside the folder containing your new blog, this is what it might look like:

```
me@penguin:~/src/my-website$ la
404.html        _config.yml  Gemfile.lock  index.markdown  _posts
about.markdown  Gemfile      .gitignore    .jekyll-cache   _site
me@penguin:~/src/my-website$ 
```

The “.markdown” files are just, as the name says, markdown files containing information regarding each specific webpage. You can, for example, open the “about.markdown” file, and start modifying it with your personal information. After that, just run

```
bundle exec jekyll serve
```

from inside the “my-website” folder, and Jekyll will update your website files, which are inside the “_site/” folder. Note that you don’t do anything with the “_site/” folder, the files in there are taken care of by Jekyll under the hood.

The “_config.yml” file will contain configuration properties used by Jekyll, such as the theme being used, the plugins that are necessary to be installed, the title of your website, and so on. We will be using a preset theme, so you won’t need to worry much about this file for now.

The “Gemfile” and “Gemfile.lock” contain information for Ruby, such as the version of Jekyll and so on. You don’t need to worry about them.

Finally, the “_posts/” folder is where you will store your posts files. This posts are markdown, so there is not much here to be said. Just follow the same structure as the example post provided, and you will be fine.

## Updating the them to enable MathJax

Unfortunately, most Jekyll themes don’t come with MathJax enabled right out of the box, so we have to do this manually, and this require that we modify the files of the theme. When hosting your blog on GitHub, some themes are natively supported (such as the minima theme), but the theme files cannot be modified this way. So we will need to bring all the theme files to the repository and modify them there.

First, let’s go to the “minima” theme GitHub repository, and then download the repository to your computer. Delete all the files in your GitHub repository containing the website, and then copy all the files from the “minima” folder to your repository. Then, run the Jekyll command to see if your site is still working. Below are the commands showing an example of how to do this:

```
cd ~/
git clone https://github.com/jekyll/minima.git
cd ./blogger.github.io
rm ./*
mv ~/minima/* ./
bundle exec jekyll serve
```

Go to the “localhost:4000” and see if your site is working properly. If it is, then stop the server, and let’s modify the theme to enable MathJax.

Open the “_layout/default.html” file (sometimes it is `_layout/base.html` for the latest *minima* theme) and add the CDN for MathJax. In other words, open “_layout/default.html” and paste this two lines in the end of the file:

```
<script type="text/javascript" id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>
```

## Writing Mathematical Equations

You are done! The only thing left to do is to actually start writing your blog posts. So let’s do an example. Open one of the posts files and write `$$ x = {-b \pm \sqrt{b^2-4ac} \over 2a} $$`.

Then, run the Jekyll to visualize your website on the localhost. This is an example of how your post should look:

$$ x = {-b \pm \sqrt{b^2-4ac} \over 2a} $$

Finally, just push all the file to your repository, and your personal mathematics blog will be on the web open and running.

## Addendum

### Adding Images to your Posts

In the root directory of "my-website", create the directory `assets/img`. Simply add any images to the `img` sub-directory and then you can add an inline image as follows:

```
![Jekyll-MathJax logo](/assets/img/jekyll-mathjax.png "Jekyll-MathJax logo")
```

### Adding a Search Bar

We are going to [Search with Lunr.js](https://jekyllcodex.org/without-plugin/search-lunr/#)

Download and save the file `search-lunr.html` in `_includes`. In this file, you can exclude the types of documents to search.

Download and save the file `lunr.js` in `assets/js` folder, then make sure that `search-lunr.html` indicates the correct location of the file. For example:

```
src="/assets/js/lunr.js"
```

cp /home/tom/.rvm/gems/ruby-2.7.1@blog/gems/minima-2.5.1/_layouts/default.html _layouts/

Inside the `_layouts/base.html` (or sometimes `default.html`) layout page, include the `search-lunr.html` as indicated in the docs inside curly percentage brackets. Add this in the `main` class, before the `content` tag.

{% include search-lunr.html %}

#### CSS for Jekyll Search

Customize the CSS for the search box. At the bottom of `search-lunr.html` there is code within `<form>...</form>`. You can wrap this in a class:

```
<div class="search">
    <form onSubmit="return lunr_search(document.getElementById('lunrsearch').value);">
        <p><input type="text" class="form-control" id="lunrsearch" name="q" maxlength="255" value="" placeholder="Search" /></p>
    </form>
</div>
```

Then in `assets/main.scss` you can try something like this:

```
.search input {
    height: 30px;
    width: 60%;
    padding-left: 10px;
    border: 1px solid #D9D9D9;
    border-radius: 10px;
    font-size: 16px;
}
```