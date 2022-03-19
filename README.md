# First, I will try something very simple, which is to use Uli's github Hello

```
Steps 1-5 is same as Uli's.
Step 6 onwards is using Google Cloud Platform Trigger
```

Run with:

`docker run -d -p 8080:8080 u1ih/hello`
- The docker run command first creates a writeable container layer over the specified image, and then starts it using the specified command. That is, docker run is equivalent to the API /containers/create then /containers/(id)/start. A stopped container can be restarted with all its previous changes intact using docker start. See docker ps -a to view a list of all containers.
- `--detach` , -d		Run container in background and print container ID
- `--publish` , -p		Publish a container's port(s) to the host
basically means to run the Docker Hub image Uli created for Hello World on port 8080. It will be replaced with whatever I want to do that I can find.


Steps:
## 1. Get Source

`git clone https://github.com/jlchiam/docker-hello`

## 2. Make Changes
From Google Cloud Shell Editor, open up docker-hello/app/index.html and make some changes.

## 3: Build Container
change into the directory: `cd docker-hello`

`docker build . -t myhello
- Build an image from a Dockerfile
- When the URL parameter points to the location of a Git repository, the repository acts as the build context. The system recursively fetches the repository and its submodules. The commit history is not preserved. A repository is first pulled into a temporary directory on your local host. After that succeeds, the directory is sent to the Docker daemon as the context. Local copy gives you the ability to access private repositories using local user credentials, VPN’s, and so forth.
- --tag , -t		Name and optionally a tag in the 'name:tag' format`

Docker will call the API to Docker Hub to get the image to build.

## 4: Run Containter
`docker run -d -p 8080:8080 myhello`

## 5: View the changes
From Google Cloud Shell, somewhere at the upper right hand side, click the "web preview" icon to see the changes.

## 6: Create a Trigger
Follow the [interactive tutorial] (https://cloud.google.com/build/docs/automate-builds)

1. Go to [Google Cloud Console] (https://console.cloud.google.com/)
2. Create a new project "docker-hello". Make sure it is selected.
3. Enable Cloud Build API
4. I have previously forked from Uli's git, so I clone using this command (replacing GITHUB_USERNAME with my github username)

```
git clone https://github.com/GITHUB_USERNAME/cloud-build-samples.git
```

5. Connect Cloud Build to Repo using Google Cloud Console. Look for "Clould Build -> Triggers". Follow the instructions in the interactive tutorial to connect.
6. Still on Google Cloud Console, on the "Triggers" page, click on "Create Trigger". Follow the instructions to create a "push" trigger.
7. I use VS Code on my desktop. Rightfully should Git Clone onto my Google Cloud Shell, but I was unsure about the Workspace organization. Hence, on my desktop, open VS Code, git clone onto my chosen directory.
8. Make a change to index.html, stage and commit the change.

   <img width="458" alt="100 docker hello index" src="https://user-images.githubusercontent.com/11884697/159124414-cadc70f2-46f6-4632-b545-efa250f0ed33.PNG">

9. On my docker-hello git hub page, open up the app folder and index.html has been changed.
    <img width="699" alt="102 docker hello changed in github" src="https://user-images.githubusercontent.com/11884697/159124545-dd86a6c7-c3ce-40aa-803f-89e3f504ec64.PNG">


10. On Google Cloud Console, go to "Cloud Build -> History" and the job has run.
    <img width="593" alt="110 docker hello job run" src="https://user-images.githubusercontent.com/11884697/159124401-2cb13f08-6a98-4d17-a1e5-45dfd4fe1bcc.PNG">




