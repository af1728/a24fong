---
layout: post
title: How I Made My Personal Website
---

The goal of this post is to provide an overview of how I, as a graduate student at the University
of Waterloo, used Jekyll to create my website and hosted it on the faculty Linux server.

Jekyll is a free static site generator. It works best for creating highly customised websites since
you can alter the styling, add scripts, and add other functionality significantly beyond what is
offered by template-based website builders, and is the way to go if you are confident with HTML and
want to make use of its blogging features.

I used a Windows device, but the steps should not vary wildly across operating systems.

### Setup

To get started, I installed
[Ruby and Jekyll](https://jekyllrb.com/docs/installation). I also (optionally) used
[Git](https://git-scm.com/downloads)—a version control system which helps us track changes in our
website, and hosted my repository on [Github](https://github.com/)—the most popular platform for
Git—you will need an account.

If you are using Github, when installing Git, set your default branch name as `main` for
consistency.

### Making the website

After installing Jekyll, I created a new directory called **website** (you can call this whatever
you like). Then I wrote a simple homepage named `index.html` within **website**. I had to learn
HTML to do this ([MDN Web Docs](https://developer.mozilla.org/en-US/docs/Learn/HTML) was a very
helpful resource).

Next I navigated to **website** in Terminal.

---

#### Aside: How to navigate in Terminal

It took me a while to figure out how to use the command line and I have not found any dedicated
resources on navigating Terminal, so I will share what I have learned in the hopes that it might
help someone like me.

Terminal is another way to navigate the computer. When you open Terminal, the last line reads
**PS C:\Users\username>**. Here **C:\Users\username** is the directory that you are in now. To go
into a subfolder—suppose that your **website** directory is in here as an example—you would type at
the end of the last line `cd website` and press Enter. The command `cd ..` allows you to go up a
directory.

Alternatively, if you have your desired directory open in File Explorer, you can right click any
blank space and click 'Run in Terminal'.

---

Then I ran the following commands:

    jekyll build
	jekyll serve

This produced the website locally and hosted it on my laptop. By running these commands after any
major changes I could see how the website will look when it is ultimately hosted at the University
of Waterloo. This also gave me a chance to debug before the website is live.

After running `jekyll build`, Jekyll will generate some folders in our project. The most important
one is **_site** which stores the generated website.

### Initialising the Git repository

As mentioned previously, I used [Github](https://github.com/) to track changes to **website** and
sync it with the University of Waterloo servers.

Switching to Terminal, I executed the following commands:

    cd _site                       # Enter _site folder
	
	# Build github repo
	git init                       # Create a Git repository skeleton
	git add --all                  # Begin tracking all files in your directory
	git commit -m "Initial commit" # Commit changes

This initialised a local git repository on my device. Next I needed to connect the local repository
to the University.

On Github, I created a new repository. The name of the repository is not important here, and you
can choose whether to have the repository be public or private. I left everything else as default.

Once this was finished, I linked the remote repository to the local one by returning to Terminal
and running the commands suggested by Github:

    git remote add origin <url-to-repository>
	git branch -M main
	git push -u origin main

I was prompted to log in to Github and authorise git-ecosystem to access the account. Now my
commits are pushed to the server!

### Hosting the website at the university Linux server

Now we need to remotely log into the University of Waterloo server to host the website.

    ssh <UWuserid>@linux.math.uwaterloo.ca # Remotely log in to server

I was prompted to enter my password, and then I was in! I could now pull the repository to the
Linux server:

	mkdir <directory-name>        # Make directory for git repository
	chmod 2755 public_html        # Restrict write access to owner
	cd <directory-name>
	git clone <url-to-repository> # Clone repository
    chmod -R 700 .git             # Restrict access to .git to owner
	cd ..

If you set your repository to public, `git clone` will simply clone the repository. If it was
private, then you will need to authenticate your Github account. Enter your username as usual, but
you will need to
[generate a personal access token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens)
to use as your password.

Now to host your website on the University of Waterloo server:

    mkdir public_html                          # Make directory for website
	chmod 2755 public_html                     # Restrict write access to owner
	cp -r <directory-name>/_site/* public_html # Copy contents of _site folder to public_html

Then the website is now visible at `https://math.uwaterloo.ca/~<UWuserid>`!

### Adding content

Jekyll has a fairly comprehensive
[step-by-step tutorial](https://jekyllrb.com/docs/step-by-step/01-setup/) on getting a blog up and
running.

After making changes or adding content to your website, commit your changes to the local Git
repository as above. Then you have to push it to Github using the command
`git push <remote> <branch>`. After that, `ssh` into the university server and use the `git pull`
command to automatically fetch and then merge the Github branch into the branch on the university
server.