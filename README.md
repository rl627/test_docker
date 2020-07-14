# test_docker

This repo contains a simple shiny app packaged as a docker. The files are organized as the follows:

```
.
+-- cmd_script.txt
+-- Dockerfile
+-- test_docker/
|   +-- test_docker.Rproj
|   +-- app.R
|   +-- renv.lock
|   +-- .Rprofile
|   +-- renv/
```
*   "cmd_script.txt": contains the lines of code that need to be run the command prompt in order to build and run the docker image.
*   "Dockerfile": is the dockerfile contains the directions for Docker to build our image. 
*   "test_docker.Rproj": this is the R project file for our app. It is beneficial to utilize R projects for packaging apps because we can not only apply version control but also utilize the renv package to easily take a precise snapshot of the software/versions used in this R project. This prevents dependence issues when building the Docker image. 
*   "app.R": Shiny app
*   "global.R" contains the pacakges required for the project
*   "renv.lock",".Rprofile","renv/": files generated by the renv package. These contain information on R/package versions and other dependency information. 

# Renv
The renv package is a new effort to bring project-local R dependency management to your projects. The goal is for renv to be a robust, stable replacement for the Packrat package, with fewer surprises and better default behaviors. This will become probably replace packrat as the golden standard for dependency management in R. More information can be found at https://rstudio.github.io/renv/articles/renv.html.

The only thing we need to do is open our Rproject and run the following two lines of code:
```
library(renv)
renv::init()
```

This will generate the files needed to build our Docker image. 