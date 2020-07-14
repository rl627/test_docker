# test_docker

This repo contains a simple shiny app and the needed files to build a Docker image. The files are organized as the follows:

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


# Docker Instaliation

Docker has two major functions. Firstly, it takes any code (any language)  and creates an image (essentially an extremely light weight virtual machine). Second, it allows the user to create instances of this image called a container. You need to install Docker Desktop (https://www.docker.com/products/docker-desktop). For windows systems  can only be done on Windows 10 Enterprise or Windows 10 Pro.  I am using Windows so perhaps you may want to use Windows version instead of apple.

After you install Docker you will interact with it using the Windows PowerShell. Windows button search "Windows PowerShell".

The first things you should do is to check that Docker was successfully installed. We can do this by running a prebuilt image that came with the software. Run the following code:

```
docker run hello-world
```

You should see a message from Docker in your command prompt that says "Hello from Docker!...."


# How to use Docker to build a Shiny apps 

After you have cloned this repo. You need to first set the this repo as your working directory. In Linux setwd() is cd. 

```
cd  C:\Users\rl627\Desktop\test_docker
```

Next step is build a docker image. Essentially, docker will look a "Dockerfile" file within the current working directory and use that as the isntructions for contructing a Docker image named test-docker. Don't forget the "." at the end; this aruggment indicates taht Docker should look within this directory. This process should take ~ 1-2 minutes because Docker needs to download all dependencies and packages. 

```
docker build -t test-docker . 
```

We can now create an isntance/container of our Docker image in order to run the shiny app.

```
docker run -d --rm -p 3838:3838 test-docker
```

This can be access from your web browser with the url "localhost:3838".

Once you are done, you need to stop the Docker contained by running

```
docker stop $(docker ps -aq)
```

