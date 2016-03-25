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

If you're using a personal repository, there is more setup involved in keeping everything synced.  For the purpose of this example, let' assume that our repo is named CO\_Map\_Gallery.



