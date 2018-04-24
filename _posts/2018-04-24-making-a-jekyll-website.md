---
layout: post
title: Making a Jekyll website
date: 2018-04-24 00:00:00 +0300
description: How to make a Jekyll site and host it for free on GitHub Pages.
img: sedona.jpg
tags: [CSS, HTML, Ruby, Markdown, About]
---

This post details how I made this website using the static site generator [Jekyll][Jekyll link], then published it with a custom domain name and hosted it for free on [GitHub Pages][GH Pages link]. Overall, this process has been excellent for me to get more familiar with how websites are made as well as with the HTML, CSS and markup languages. Furthermore, as I now have a platform to make content that is my own, it has helped and will help me to reinforce the learning experiences I have, as teaching something is a great way to learn it.

#### Why Jekyll and GitHub Pages?

My experience with making websites is pretty much non-existent, therefore when I set out to build a personal website I was not particularly confident with how to design, build or implement the different aspects of a website. A friend of mine recommended that I use the static site generator Jekyll, as it does most of the heavy lifting for you and lets you concentrate on just making the content for the site.

From my perspective, the main advantage of using Jekyll is that it is free and there are loads of free themes which you can use to make your site look great. Furthermore, as it is a static site generator, the website is very quick and responsive. All the files for the website are generated beforehand and then served to a user when they are on the site, this is different from a dynamic generator which generates files for the site for each user, slowing the delivery of pages to your browser. Finally, as all the files are static, there is much less chance of your site being hacked or suffering from a security breach.

GitHub Pages is a free service run by GitHub which allows users to host a website through a GitHub repository. Jekyll websites are supported by GitHub and so this means that the hosting costs for the website are zero. You also benefit from the security of being hosted by GitHub's servers which are probably never going to go down. Finally, it helps you to learn and implement git so that you can have version control on your site.

So to summarise, using Jekyll and GitHub Pages you can have a fast website, that looks great and is free to host, with the added benefit of being very secure.

#### Installing Jekyll and generating a site

To install Jekyll I would recommend referring to the installation guide specific to your operating system on the [offical website][Jekyll link]. If you are having trouble installing, then take a look at their [help pages][Jekyll help], I ran into trouble as a Mac update had uninstalled my command line tools. So make sure these are up to date if you are having any issues.

Once it is installed you can then create a new site and test it out. Simply enter the following commands to the terminal.

{% highlight bash %}
~ $ jekyll new my-awesome-site
~ $ cd my-awesome-site
~/my-awesome-site $ bundle exec jekyll serve
{% endhighlight %}

This will compile the default Jekyll site which can give you a feel for the different ways you can customise it. The output from that final command should display a server address which you can paste into your internet browser to view the site. The actual website itself is held in the '_sites' directory. You can edit the '_config.yml' and 'Gemfile' files to change the name of the site and other details. The '_posts' directory is where you can add content to the site in terms of blog posts, which is done as [Markdown][markdown link] files. The advantage of these is that again you can just get on with writing the content and the formatting is taken care of for you, a little bit like [LaTeX][Latex link], the language popular in academia for writing scientific papers.

I should also mention that although I have used Jekyll, [other static site generators are available][other site generators].


#### Picking and installing a theme

If you have a good idea for the kind of content or design you want to have in your site it is probably best to stop playing around with the default Jekyll site and find a good theme that you think fits in with what you want to do. There are thousands of themes out there and using google you can find lots of sites with lists of themes you can preview (e.g. <https://jekyll-themes.com>).

To install the theme you can simply clone the repository for the site. To do this it is best to get a [GitHub account][how to get github] if you don't have one already and [install git][how to install git] on your computer. Then you can download the theme by going to the repository page on GitHub (which should be linked to where you found the theme), then click the 'Clone or download' button and copy the address. Open a terminal window and run the following commands:

{% highlight bash %}
git clone "paste address here"
{% endhighlight %}

For example, if you wanted to clone this website you would run:
{% highlight bash %}
git clone https://github.com/H-Cox/H-Cox.github.io.git
{% endhighlight %}

You should then change directory to the newly cloned repository. Once you are in the new directory you can attempt to run the site again using 'bundle exec jekyll serve', however, you might get an error. This is probably because the theme uses plugins you have not got installed. To remedy this you can install the missing packages using

{% highlight bash %}
bundle install
{% endhighlight %}

which should install any missing plugins.

#### Modifying the theme and creating content

Now you have the theme running you will want to make the site your own, for example changing details in the config and Gemfile files. To do more fundamental changes to the site you might want to edit the HTML or CSS files in the 'assets' and 'layouts' folders. In my case, I used the [flexible-jekyll][flexible-jekyll] theme, which by default doesn't have any links in the sidebar. To add the links in, I edited the 'main.html' file in the 'layouts' folder to include additional information in the sidebar.

It might be a good idea to check out other themes and clone them as well, then you can start to build up an understanding of how different aspects of each theme are implemented. In this way you can start to make a site which is exactly as you like.

To create content such as blog posts you will need to get familiar with the markup language [Markdown][markdown link]. So long as you format the file correctly, and follow the convention for naming your files in the 'posts' folder - 'YYYY-MM-DD-post-title.md', then the posts should start automatically appearing in the site. If a post date is in the future then it won't show until the actual date passes it.

As you are creating content and changing settings on your site remember to keep testing and building the site to ensure it is still working as you expect. If everything breaks you can always just delete the whole directory and then clone the original repository again.

#### Getting the site online

Once you have the site working and looking as you would like, you can publish it using GitHub Pages. Follow the [instructions][GH Pages link] to create and clone your GitHub Pages repository so that it is on your PC. Once you have got the basic "Hello, world" site up and running using the instructions you can copy your site and commit it to GitHub.

To do this the simplest way is to copy all files (not hidden files) from the directory of your site, to the new repository directory you have just created by cloning your new GitHub Pages repository. Now change directory to the GitHub Pages repository on your PC and check the website is built as you expect, using the 'bundle exec jekyll serve' command as before.

If you are happy with the site at this point all you need to do is commit the changes and push them to GitHub.

{% highlight bash %}
git add --all
git commit -m "Enter a message"
git push
{% endhighlight %}

You should now be able to go on your internet browser and go to https://username.github.io, where you replace username with your GitHub username and see the site in action.

#### Using custom domain name

To add an extra element of professionalism to your new website you might want to register a custom domain name which people can use to access your site. This is the only part you will need to spend money on, however it is not that expensive. There are many different domain name registration services out there, the one I used was <https://www.namecheap.com>. 

Once you have bought your domain name, you need to change a few settings to link the GitHub Pages site to your custom address.

First go into the settings of your GitHub Pages repository online and change the custom domain setting to the new domain name you have just registered. Once you click save, verify that it has created a new file called 'CNAME' in the repository and that the file contains the new domain name.

Next, you need to tell your domain service provide (namecheap in my case) to send people to your GitHub site. To do this you need to add three entries to the 'Advanced DNS' settings of the domain details. The details of these along with a more complete tutorial of the whole process is shown [here][Namecheap DNS].

#### Finishing touches

Hopefully, you will now have a fully functioning Jekyll site, running on your custom domain. If you have any trouble with this along the way, google is your friend, and a quick search should bring up a solution or workaround you can implement. To help you maintain a working site in future one thing you might want to consider is creating a separate development branch of your site repository on GitHub. This way you can make changes to the site and push them to GitHub, safe in the knowledge that they won't break anything. Then, when you are sure you want them, you can merge them into the master branch and they will go live.

To do this, first make sure you are currently up to date with the master branch by entering 'git status' in the terminal. If there are any untracked changes now is the time to commit them and push them to the online repository, as before.

Next, create a new branch, this can be named anything but I have used development here.

{% highlight bash %}
git checkout -b development
{% endhighlight %}

This also switches you to the development branch. Now you will want to commit and push the new branch online. Once you have done this, run the 'git status' command again to ensure everything is up to date.

Now you have the branch set up, you can make changes to the site here and commit them to the repository as normal. When you are ready to merge the changes into the live site you first change back to the master branch, and then merge the branches.

{% highlight bash %}
git checkout master
git merge development
{% endhighlight %}

Now you just need to check everything is working as expected and then run the 'git push' command to implement the changes to the live site.

I hope you have learned something from this post, if there are any mistakes then please let me know.

Photo: The red rocks of Sedona, Arizona, USA.

[Jekyll link]: https://jekyllrb.com
[GH Pages link]: https://pages.github.com
[Jekyll help]: https://jekyllrb.com/docs/troubleshooting/
[Latex link]: https://en.wikipedia.org/wiki/LaTeX
[markdown link]: https://www.markdownguide.org/getting-started
[other site generators]: https://www.staticgen.com
[flexible-jekyll]: https://github.com/artemsheludko/flexible-jekyll
[how to install git]: https://linode.com/docs/development/version-control/how-to-install-git-on-linux-mac-and-windows/
[how to get github]: https://github.com
[Namecheap DNS]: https://www.namecheap.com/support/knowledgebase/article.aspx/9645/2208/how-do-i-link-my-domain-to-github-pages