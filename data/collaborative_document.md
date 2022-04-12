![](https://i.imgur.com/iywjz8s.png)


# Collaborative Document

## 2022-04-06 Introduction to Docker

# https://tinyurl.com/2022-04-06-docker

Welcome to The Workshop Collaborative Document.

This Document is synchronized as you type, so that everyone viewing this page sees the same text. This allows you to collaborate seamlessly on documents.

----------------------------------------------------------------------------

This is the Document for today: [link](https://tinyurl.com/2022-04-06-docker)


## 👮Code of Conduct

* Participants are expected to follow those guidelines:
* Use welcoming and inclusive language.
* Be respectful of different viewpoints and experiences.
* Gracefully accept constructive criticism.
* Focus on what is best for the community.
* Show courtesy and respect towards other community members.
 
## ⚖️ License

All content is publicly available under the Creative Commons Attribution License: [creativecommons.org/licenses/by/4.0/](https://creativecommons.org/licenses/by/4.0/).

## About Us
https://www.esciencecenter.nl

### Digital Skills Workshops
https://esciencecenter-digital-skills.github.io

### NL-RSE
https://www.nl-rse.org

### Upcoming events
|Workshop|Date|Location|Registration|
|-|-|-|-|
|GPU Programming|11 May 2022|Amsterdam|registration opens 19 April|
|Parallel Programming in Python| 17 - 18 May 2022| Amsterdam|registration opens 26 April|
|Data Carpentry for Social Sciences with Python| 30 May - 2 June| online | |

### Updates
To keep up to date with all our Training & Workshops go to
https://tinyurl.com/w6zyt867
and select "Training and Workshops newsletter"


## 🙋Getting help

You can use the blue post-it (or ask questions in the document).

## 🖥 Workshop website

[link](https://esciencecenter-digital-skills.github.io/2022-04-06-ds-docker/)

🛠 Setup

[link](https://esciencecenter-digital-skills.github.io/2022-04-06-ds-docker/#setup)


## 👩‍🏫👩‍💻🎓 Instructors

Djura Smits, Johan Hidding

## 🧑‍🙋 Helpers

Cunliang Geng, Francesco Nattino


## 🗓️ Agenda
| | |
|--|--|
|9:30|Welcome and Icebreaker|
|9:45|Introducing Containers|
|10:30|Break|
|10:40|Introducing the Docker Command Line|
|11:00|Exploring and Running Containers|
|11:30|Break|
|11:40|Cleaning up containers|
|12:05|Docker hub|
|12:30|Lunch Break|
|13:30|Creating Your Own Container Images|
|14:30|Break|
|14:40|Creating more complex container images|
|15:30|Break|
|15:40|Containers in Research Workflows: Reproducibility and Granularity|
|16:15|Wrap-up|
|16:30|Drinks!|

## 🔧 Exercises

### 1. EXPLORING A COMMAND

Run `docker --help` and pick a command from the list. Explore the help prompt for that command. Try to guess how a command would work by looking at the `Usage:` section of the prompt.

### 2. CHECK ON YOUR IMAGES
What command would you use to see if the `hello-world` Docker container image had downloaded successfully and was on your computer? Give it a try before checking the solution.

*Solution:* `docker image ls`

### 3. HELLO WORLD, PART 2
Can you run a copy of the `alpine` container and make it print a “hello world” message?

*Solution:* `docker container run alpine echo "Hello world"`

### 4. PRACTICE MAKES PERFECT
Can you find out the version of Ubuntu installed on the `ubuntu` container image? (Hint: You can use the same command as used to find the version of alpine.)

Can you also find the apt-get program? What does it do? (Hint: try passing --help to almost any command will give you more information.)

*Solution:* `docker container run ubuntu cat /etc/os-release`

### 5. WHAT’S IN A NAME?

How would I download the Docker container image produced by the rocker group that has version 3.6.1 of R and the `tidyverse` installed?

Note: the container image described in this exercise is large and won’t be used later in this lesson, so you don’t actually need to pull the container image – constructing the correct `docker pull` command is sufficient.

*Solution:* `docker pulll rocker/tidyverse:3.6.1`

### 6. SEARCHING FOR HELP

Can you find instructions for installing R on Alpine Linux? Do they work?

### 7. TAKE A GUESS

Do you have any ideas about what we should use to fill in the sample `Dockerfile` to replicate the installation we did above (i.e. install python in alpine)?

*solution:*

Dockerfile:
```shell
FROM alpine:latest
RUN apk add --update python3 py3-pip python3-dev
RUN pip install click
CMD ["python3"]
```
Build image with:
```shell=
docker image build -t python-click .
```
Run with:
```shell=
docker run -it python-click
```

### 8. REVIEW!
1. Think back to earlier. What command can you run to check if your container image was created successfully? (Hint: what command shows the container images on your computer?)
2. We didn’t specify a tag for our container image name. What tag did Docker automatically use?
3. What command will run a container based on the container image you’ve created? What should happen by default if you run such a container? Can you make it do something different, like print “hello world”?

Solution:
1. `docker image ls`
2. `latest`
3. `docker container run python-click echo "hello world"`

### 9. DID IT WORK?
Can you remember how to run a container interactively? Try that with this one. Once inside, try running the Python script.

*Solution:* 

```shell
docker container run -it sum-py sh
$ cd /app
$ python3 sum.py 4 5
```


## 🧠 Collaborative Notes

### How can containers be useful to you?

Examples:
* Portability (use same software on different platforms);
* Reproducibility (keep running version of software in future).

### Docker Hub

Docker Hub: hub.docker.com

Host images which we have pulled. Official images are managed by Docker team.

Example page for `python` docker image: https://hub.docker.com/_/python

## On building images

* Start on images that are already available.
* Size matters - different installation procedures might lead to different sizes

## Command log

Test whether docker is installed/which version I have:
```shell=
docker --version
```

Which containers are running:
```shell=
docker container ls
```

How to get help:
```shell=
docker --help
```

Help about subcommands:
```shell=
docker container --help
docker container ls --help  # and so on
```

Which docker images are available:
```shell=
docker image ls
```

Download image:
```shell=
docker image pull hello-world
docker image ls  # show that image is downloaded
```

Run container:
```shell=
docker container run hello-world
```

Running container from image that is not locally available will dowload the image first:
```shell=
docker container run alpine
```

Run some commands in the container:
```shell=
docker container run alpine cat /etc/os-release
```

Run container interactively (will give you a prompt inside the container):
```shell=
docker container run -it alpine sh
$ ls
<will show directory content inside container>
$ pwd
/
$ whoami
root
$ cat /etc/os-release
< ... > 
$ exit  # to close and shut down container
```

Remove images (you can get the list of images/IDs with `docker image ls`):
```shell=
docker image rm <IMAGE_ID>
```

But first I need to delete the containers based on the image I want to delete. Check containers with `docker container ls --all`, then remove them with:
```shell=
docker container rm <CONTAINER_ID>  # delete single container
```
or 
```shell=
docker container prune  # delete all stopped container
```

Pull python image:
```shell=
docker image pull python
```

Let's install python in an alpine image:

```shell=
docker container run -it alpine
# run the following inside the container
$ apk add --update python3 py3-pip python3-dev
$ python3 --version
# Python 3.9.7
$ pip installl click
$ exit  # exit and shutdown container
```

Reproducible way to build container: write `Dockerfile`!

Create file called `Dockerfile` with the following content:
```shell=
FROM alpine:latest
RUN .. some command ...
RUN
CMD ["ls", "-lF", "/etc"]
```

Build image from `Dockerfile` (in the same directory):
```shell=
docker image build -t ls-test .
```

Run docker container with:
```shell=
docker run ls-test
```

Example of Dockerfile to install python in alpine image - see solution of Exercise 7.

Login on Docker Hub:
```shell=
docker login
# fill in username and password
```

Build image with name that is compatible with Docker Hub naming convention:
```shell=
docker image build -t <USERNAME>/<IMAGE_NAME>:<TAG>
# e.g. docker image build -t djoerzilla/useless:v1 .
```
Or add tag to already existing image:
```shell=
docker tag <IMAGE_NAME>:<TAG_NAME> <NEW_IMAGE_NAME>:<NEW_TAG_NAME>
# e.g. docker tag python-click djoerzilla/useless:v1 
```

Then push image to Docker Hub:
```shell=
docker push <USERNAME>/<IMAGE_NAME>:<TAG>
# e.g. docker push djoerzilla/useless:v1
```

Create new directory with file `sum.py`:
```python=
#!/usr/bin/env python3

import sys
try:
    total = sum(int(arg) for arg in sys.argv[1:])
    print('sum =', total)
except ValueError:
    print('Please supply integer arguments')
```

We want to use the `python:slim` image to run the Python script above:

```shell=
docker container run python:slim python3 sum.py 
# ERROR - script is outside container!
```

One solution: add script to docker image. Create new `Dockerfile`:
```shell
FROM python:slim
RUN mkdir /app
COPY sum.py /app/
```

Now we build the image:
```shell=
docker image builld -t sum-py .
```
and run the container:
```shell=
docker container run sum-py python3 /app/sum.py
```

You can also clone repository in a new image (or do any other action):
```
FROM python:alpine
RUN mkdir /app
RUN apk add git
RUN git clone https://github.com/dsmits/docker-exercises.git
COPY sum.py /app/
```
Build again:
```shell=
docker image build -t sum-py . 
```
Run container interactively:
```shell=
docker container run -it sum-py sh
```

Share part of the host filesystem with the container:
```shell=
docker container run --mount type=bind,source=/PATH/OF/THE/DIR,target=/johan python:alpine python3 /johan/sum.py
```
(on linux/mac use ${PWD} for getting path of current directory)
(on windows, you can copy the whole C://... path from file explorer or use %cd% for getting the path automatically)

To run as different user (for instance when creating file in a mounted host directory) - use `docker run -u <USERNAME>`

### Example: Run Docker image as GitHub Actions

Full example: https://esciencecenter-digital-skills.github.io/docker-introduction/e01-github-actions/

Let's create a website using `pandoc`, based on markdown file README.md - example: https://github.com/jhidding/readme-pages


* Create new repository on GitHub, with a README.md file and a license (Apache-2.0).
* Clone the repository locally
* Get `pandoc` image: 
```shell=
docker run pandoc/core --version
```
* Run pandoc on README file:
```shell=
docker run --mount type=bind,source=${PWD},target=/tmp  pandoc/core tmp/README.md -s --output=/tmp/bbuild/index.html
```
* After modifying README.md, commit and push to repository
```shell=
git add README.md
git commit -m "modified README"
```
* Add workflow on GitHub Actions tab (click New). On `push`, runs on `ubuntu-latest`, add step:
```yaml
- name: Prepare build environment
  run: |
    mkdir -p build
    touch build/.nojekyll 
    
- name: Run pandoc
  uses: docker://pandoc/core:2.18
  with: 
    args: >-
      --standalone
      --output=build/index.html
      README.md

- name: Deploy on GH pages
  uses: JamesIves/github-pages-deploy-action@4.1.0
  with:
    branch: gh-pages
    folder: build
```



## 📚 Resources
* [Introduction slides](https://esciencecenter-digital-skills.github.io/containers-presentation)
* [Linux command tutorial (beginner level)](https://linuxcommand.org/)
* [How does Docker run a Linux kernel under macOS host?](https://stackoverflow.com/questions/43383276/how-does-docker-run-a-linux-kernel-under-macos-host)
* [Notes about Docker security](https://docs.docker.com/engine/security/)
* [Reference on Dockerfile](https://docs.docker.com/engine/reference/builder/)
* [Docker examples](https://esciencecenter-digital-skills.github.io/docker-introduction/docker-image-examples/index.html)
* [Lesson Material](https://esciencecenter-digital-skills.github.io/docker-introduction/) 
* [**POST WORKSHOP SURVEY**](https://www.surveymonkey.com/r/BHVHC5L)
