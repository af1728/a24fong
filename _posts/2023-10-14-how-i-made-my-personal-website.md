---
layout: post
title: How I made my personal website
tag: tutorial
tag: website
---

The goal of this post is to walk through, from start to finish, how a graduate student at the
University of Waterloo (who is, like me, semi-comfortable with coding in principle only) can use
Jekyll to create a website and host it on the faculty Linux server.

Jekyll is a free static site generator. It works best for creating highly customised websites since
you can alter the styling, add scripts, and add other functionality significantly beyond what is
offered by template-based website builders, and is the way to go if you are comfortable using HTML
and want to make use of its blogging features.

I will try to make this tutorial as generic as possible, but the hosting instructions is (as far as
I know) specific to Waterloo. I also used a Windows device, but the steps should not vary wildly
across operating systems.

### Setup

To get started, you will need to make sure you have a copy of
[Ruby and Jekyll](https://jekyllrb.com/docs/installation). Optionally (but strongly recommended),
you can use [Git](https://git-scm.com/downloads)—a version control system which helps us track
changes in our website, and host your repository on [Github](https://github.com/)—the most popular
platform for Git—you will need an account.

If you are using Github, when installing Git, set your default branch name as `main`, as this is
the default name used by Github.

### Making the website

After installing Jekyll, create a new directory called **website** (you can call this whatever
you like). To ensure the website works on the servers provided by the University of Waterloo, we
will need to set the base url in a configuration file. Create `_config.yml` in **website** with the
following content:

```yaml
baseurl: /~<UWuserid>
```

Then you can create a simple webpage in HTML, and name it `index.html` within **website**.
([MDN Web Docs](https://developer.mozilla.org/en-US/docs/Learn/HTML) is a very helpful resource for
learning HTML). Note: this is the file name that all web browsers look for unless the filename is
indicated in the URL.

Next we navigate to **website** in Terminal.

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

Then we should run the following commands:

```powershell
jekyll build
jekyll serve
```

This will produce the website locally and host it on your device. By running these commands after
any major changes we can see how the website will look when it is ultimately hosted at the
University of Waterloo. This will also give us a chance to debug before the website is live.

After running `jekyll build`, Jekyll will generate some folders in our project. The most important
one is **_site** which stores the generated website.

### Initialising the Git repository

As mentioned previously, we will use [Github](https://github.com/) to track changes to **website**
and sync it with the University of Waterloo servers. Switching to Terminal, we execute the
following commands:

```powershell
cd _site                       # Enter _site folder
	
# Build github repo
git init                       # Create a Git repository skeleton
git add --all                  # Begin tracking all files in your directory
git commit -m "Initial commit" # Commit changes
```

This initialises a local git repository on your device. Next we need to connect the local
repository to the University.

On Github, we will create a new repository. The name of the repository is not important here. For
simplicity later, I recommend leaving the repository public, but I have included specific
instructions if you set it to private. You can leave everything else as default.

Once this is finished, link the remote repository to the local one by returning to Terminal and
running the commands suggested by Github:

```powershell
git remote add origin <url-to-repository>
git branch -M main
git push -u origin main
```

You will be prompted to log in to Github and authorise git-ecosystem to access the account. Now
your commits are pushed to the server!

### Hosting the website at the university Linux server

Now we need to log on to our Unix account to host the website. To connect from off-campus, you will
need to run the [campus
VPN](https://uwaterloo.atlassian.net/wiki/spaces/ISTSERV/pages/42588307544/About+the+Virtual+Private+Network+VPN).
Then remotely log into the server:

```powershell
ssh <UWuserid>@linux.math.uwaterloo.ca # Remotely log in to server
```

Enter your WatIAM password, and then you will be in the faculty server! We can now pull the
repository to the Linux server (note that the name on the Github repository will be the name of
your directory):

```powershell
git clone <url-to-repository> # Clone repository
cd <repository-name>
chmod -R 700 .git             # Restrict access to .git to owner
cd ..
```

If you set your repository to public, `git clone` will simply clone the repository. If it was
private, then you will need to authenticate your Github account. You can enter your username as
usual, but you will need to
[generate a personal access token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens)
to use as your password.

Now to host your website on the University of Waterloo server:

```powershell
mkdir public_html                               # Create directory for website
chmod 2755 public_html                          # Restrict write access to owner
rsync -avuP <directory-name>/_site/ public_html # Synchronises contents of _site folder with public_html
```
	
To view the list of files with permissions, use the command `ls -l`. The permissions in front of
your **public_html** folder should read `drwxr-sr-x`.

You should see your website at `https://math.uwaterloo.ca/~<UWuserid>`. Moreover, the website should
look identical to the one we built and served locally.

Type `logout` to sever your connection to the server.

### Adding content

Jekyll has a fairly comprehensive
[step-by-step tutorial](https://jekyllrb.com/docs/step-by-step/01-setup/) on getting a blog up and
running.

After making changes or adding content to the website, we can commit our changes to the local Git
repository as above. Then we have to push it to Github using the command
`git push origin main`. After that, `ssh` into the university server and use the
`git pull origin main` command to automatically fetch and then merge the Github branch into the
branch on the university server. You can use the same command as above to replace the existing
website with the updated one.