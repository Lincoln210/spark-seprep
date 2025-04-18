## Prerequisite

Ensure that you are up to date with the upstream Github repo. Do the following before starting your assignment.

```
cd <to your github repo path>
git checkout main
git fetch upstream
git rebase upstream/main
git checkout -b assignment7 upstream/main
```

## Write a Script or Program

Write a script or a program that gives you an output - it can be anything! You can write it in python, bash, C, Go etc.
We just want something that gives us an output that runs, but feel free to go all out and create something amazing!

You can also use the python script you wrote when solving the Leetcode problem from the last assignment. Just update it to give you an output.

## Create a Containerfile

Head to the directory **student-work/assignment-7** and create a directory there with your name in the format **FIRSTNAME-LASTNAME**.
The directory should be **student-work/assignment-7/[FIRSTNAME-LASTNAME]** so you can add your Containerfile and script there.


Create a Containerfile to package the script you just wrote. Set the **CMD** of your container image to call your executable file.

```
...
CMD ./path/to/your/executable
...
```

This is what an example Containerfile looks like
```
FROM alpine
WORKDIR mydir
ADD joke.sh /mydir
RUN chmod +x /mydir/joke.sh
RUN apk add curl
CMD ./joke.sh
```
Head to https://docs.docker.com/get-started/02_our_app/ for a quick tutorial on Containerfiles/Dockerfiles. Google is your friend, use it!

Look at [https://github.com/DS219/spark-seprep/tree/main/assignments/assignment5/urvashi-mohnani](https://github.com/DS219/spark-seprep/tree/main/student-work/assignment-7/urvashi-mohnani) as an example!
Do not use the exact same script and Containerfile for your assignment, you will not get any points if you do!

## Build and tag your container image

```
cd student-work/assignment-7/[FIRSTNAME-LASTNAME]
podman build -t [image-name] -f [path/to/containerfile] .
```

## Create a free account on Docker hub if you don't already have one

Head to Docker hub (https://hub.docker.com/) and create a free account there. Make sure to remember your username and password!

## Push the built container image to your docker hub account

Login to the docker hub account you created above with podman and enter the username and password when prompted.
```
podman login docker.io
```

Now you can push the image you built to your docker hub account.
```
podman push [image-name] docker.io/[username]/[image-name]
```

Make sure to run your container image with podman to ensure it runs successfully!
```
podman run [image-name]
```
If your script is interactive and requires user input, you need to enable the interactive and tty flags so you are able to send this input to the container. Use this command to run your container instead:
```
podman run -it [image-name]
```

Add your container image name to this doc https://docs.google.com/document/d/1_mJ-SAgSAZK23kNLbsonv8uKrhqK-o6bXNTV-V7vWik/edit?usp=sharing.
Make sure it is the full qualified image name in the format **docker.io/[your-username]/[your-imagename]**.

## Run a classmate's container image locally

Look through the doc above and pick a container image that one of your classmate's built. Pull it down and run it locally on your machine.

```
podman pull [classmate-image]
podman run [classmate-image]
```

Create your PR on Github and answer the questions in this [form](https://forms.gle/WS8W7bo9tEEoDtTf8) and hit submit!

**Note:** Always check the files that you are comitting in your working tree before actually comitting. For this assignment, you only need 2
files - your Containerfile and your script. Do not commit any extra files. The following command will show you your working tree always.
```
git status
```

**Grading Rubric:**
- Answered form questions (4 pts)
- Container image built runs successfully (2 pts)
- Containerfile syntax and format is correct (2 pts)
- Containerfile only has exactly what your script needs to run i.e no extra packages and files installed (2 pts)
- Descriptive and clear commit message (2 pts)
- Only 1 commit in your PR (2 pts)
- No extra junk files in PR (2 pts)
- Changes should be done on the assignment branch and not on main (2 pts)
- No modifications to any other files in the repo (2 pts)
