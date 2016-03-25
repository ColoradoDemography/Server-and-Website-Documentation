# How to Add an Application

**This tutorial assumes that you've got your application in a Github repository.**


- Fork the repository to the organization (if it's not already located there)

- Add a new branch to your project called 'gh-pages'

![Add Github Branch](/img/add-branch.jpg)

- after a minute or so, point your web browser to https://demography.dola.colorado.gov/ProjectName/if-needed.html



### Updating the Application

#### When using an original ```coloradodemography``` repository

Typically, when using Github on the command line, you would type ```git push``` to push your committed changes to your repository.  Consider that this would be short for ```git push master```.
From now on, type: ```git push master``` and ```git push gh-pages``` to update both the main branch of your repository, and your published version (on gh-pages).

#### When using a 'forked' personal repository

If you're using a personal repository, there is more setup involved in keeping everything sync'd.  For the purpose of this example, let' assume that our repo is named CO\_Map\_Gallery.

First, type ```git remote -v``` to take a look at your current remote repositories.  You'll probably be looking at something similar to this:

![See remote branches](/img/git-remote-1.jpg)

We're going to need to add an upstream remote to 'push' changes to.  

We'll find the link for the forked repo on our organization account

![Find Link](/img/git-remote-7.jpg)

...and use that to establish a new remote.

![Add remote branch](/img/git-remote-2.jpg)

There, that will add a remote that we've called 'codemog' which will point to the forked repository in the organization directory.

![Verify remote branch](/img/git-remote-6.jpg)

Now, let's test this out.  We'll make a small change to our personal version of the repository and see if we can push that into our organization repository.

![Small change](/img/git-remote-3.jpg)

So we've made a small change by adding some text to the bottom of the extracontent.html page of the repository.  Let's commit and push that change.

![Small change](/img/git-remote-4.jpg)

After committing the change (in the usual way), our push step becomes a series of 3 commands:

```git push origin master``` which updates our local repository

```git push codemog master``` which updates our remote repository on our organization account

```git push codemog master:gh-pages``` which push the organization master branch to the organization gh-pages (published) branch


And, for your verification.

![verification](/img/git-remote-5.jpg)

There's probably a better way to do this...

