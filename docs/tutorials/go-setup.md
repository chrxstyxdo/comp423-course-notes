# Setting up a dev container for Go
* Primary author: [Christina Do](https://github.com/chrxstyxdo)
* Reviewer: [Minh Nguyen](https://github.com/mp-nguyen26)

## Prerequisites
Make sure you have:  
1. **A GiHub account**: If you don’t have one yet, sign up at [GitHub](https://github.com).  
2. **Git installed**: [Install Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) if you don’t already have it.  
3. **Visual Studio Code (VS Code)**: Download and install it from [here](https://code.visualstudio.com/).  
4. **Docker installed**: Required to run the dev container. [Get Docker here](https://www.docker.com/products/docker-desktop/).  
5. **Command-line basics**: Your COMP211 command-line knowledge will serve you well here. If in doubt, review the Learn a CLI text!  

## Project Setup: Part One: Creating the Repository

### Step 1: Create a Local Directory and Initialize Git

1. Open your terminal or command prompt.
2. Create a new directory for your project. 
```
mkdir comp423-go-project
cd comp423-go-project
```
3. Initialize a new Git repository:
```
git init
```
4. Create a README file:
```
echo "# COMP423 Go Project" > README.md
git add README.md
git commit -m "Initial commit with README"
```

### Step 2: Create a Remote Repository on GitHub

1. Log in to your GitHub account and navigate to the [Create a New Repository](https://github.com/new) page.
2. Fill in the details as follows:
    *  **Repository Name**: ``` comp423-go-project```
    *  **Description**: Setting up a new DevContainer project in Go Language
    *  **Visibility**: Public
3. Do not initialize the repository with a README, .gitignore, or license.
4. Click **Create Repository**.

### Step 3. Link your Local Repository to GitHub

1.  Add the GitHub repository as a remote:
```
git remote add origin https://github.com/<your-username>/comp423-go-project.git
```
Replace ```<your-username>``` with your GitHub username.
2. Check your default branch name with the subcommand ```git branch```. If it's not ```main```, rename it to ```main``` with the following command: ```git branch -M main```. Old versions of ```git``` choose the name ```master``` for the primary branch, but these days ```main``` is the standard primary branch name.
3. Push your local commits to the GitHub repository:
```
git push --set-upstream origin main
```

    !!! info "Understanding the --set-upstream Flag"
        * ```git push --set-upstream origin main```: This command pushes the main branch to the remote repository origin. The ```--set-upstream``` flag sets up the main branch to track the remote branch, meaning future pushes and pulls can be done without specifying the branch name and just writing ```git push origin``` when working on your local ```main``` branch. This long flag has a corresponding ```-u``` short flag.

4. Back in your web browser, refresh your GitHub repository to see that the same commit you made locally has now been pushed to remote. You can use ```git log``` locally to see the commit ID and message which should match the ID of the most recent commit on GitHub. This is the result of pushing your changes to your remote repository.

## Part 2. Setting Up the Development Environment

### Step 1. Add Development Container Configuration

1. In VS Code, open the ```comp423-go-project directory```. You can do this via: File > Open Folder.
2. Install the **Dev Containers** extension for VS Code.
3. Create a ```.devcontainer directory``` in the root of your project with the following file inside of this "hidden" configuration directory:  
```.devcontainer/devcontainer.json```
The devcontainer.json file defines the configuration for your development environment. Here, we're specifying the following:  
    * ```name```: A descriptive name for your dev container.
    * ```image```: The Docker image to use, in this case, the latest version of a Go environment. Microsoft maintains a collection of base images for many programming language environments, but you can also create your own!
    * ```customizations```: Adds useful configurations to VS Code, like installing the Go extension. When you search for VSCode extensions on the marketplace, you will find the string identifier of each extension in its sidebar. Adding extensions here ensures other developers on your project have them installed in their dev containers automatically.
    * ```postCreateCommand```: A command to run after the container is created.

    ```
    {
    "name": "COMP423 Course Notes",
    "image": "mcr.microsoft.com/vscode/devcontainers/go",
    "customizations": {
        "vscode": {
        "settings": {},
        "extensions": ["golang.go"]
        }
    },
    "postCreateCommand": "go mod download"
    }
    ```

### Step 2. Reopen the Project in a VSCode Dev Container
Reopen the project in the container by pressing ```Ctrl+Shift+P``` (or ```Cmd+Shift+P``` on Mac), typing "Dev Containers: Reopen in Container," and selecting the option. This may take a few minutes while the image is downloaded and the requirements are installed.

Once your dev container setup completes, close the current terminal tab (trash can), open a new terminal pane within VSCode, and try running ```go version``` to see your dev container is running a recent version of Go.




