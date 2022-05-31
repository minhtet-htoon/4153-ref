# Git Install and Usage

## What is Git?
Git is a source control system that allows multiple developers to work asynchronously on a project. It does this by 
tracking changes to individual files in a folder called a repository then uploading it to the cloud. From there, another
developer can download it, make changes and push it back to the cloud.

## What is GitHub
GitHub is a website where developers store and share code in the form of git repositories

## Git Install
1. Linux
   1. Almost all distros come with it by default. 
   2. If yours doesn't, ~~switch distros~~, install it using your package manager. The package is probably called `git`
2. MacOS
   1. Install via homebrew
      1. Simply run `brew install git`. Assuming you have homebrew installed
   2. Install with XCode
      1. Install XCode from the App Store, contains git
3. Windows
   1. Go to [git's website](https://git-scm.com)
   2. Download the Windows .exe installer
   3. Run the installer
   4. Open your terminal and run `git --version` If an error is thrown, follow the next step. If not, you're ready to go
   5. Add it to PATH
      1. Left-click on the Windows Start Menu and Click on the gear icon to open windows settings.
      2. In the “Windows Settings” window, search for "System Environment Variable".
      3. Now select "Edit the system environment variables".
      4. Next, click the "Environment Variables" button at the bottom-right on the System Properties dialog box.
      5. Double-click on the "Path" entry under "System variables". If you wish to do it for yourself then double-click on the “Path” entry under your User.
      6. Next, click on "New" button and add the following two paths  C:\Program Files\Git\bin\ and C:\Program Files\Git\cmd\ to the end of the list.
      7. Close all open windows
      8. Finally, close and re-open your PowerShell or Command Prompt to reload Path variables.
      9. Try `git --version` to see if it works this time
## Using Git 

### Initialize a repository
To begin using git, simply navigate to an empty folder using `cd`. For this tutorial, I'll be using a system running 
Manjaro Linux. The only major difference you need to care about is that Windows uses a backslash instead of a forward
slash to delimit directories. Ex. `C:\Users\minhteth\Documents` on Windows ≡ `/home/minhteth/Documents` on Linux

Begin by initializing a git repository using the `git init` command. This will create a hidden directory called `.git`
It's contents don't matter to us. 

### Adding Files
Running `git add <file_name>` will tell git to track the changes in that file. The command `git add *` will add all 
files in that directory to git. 

### .gitignore
Of course, you don't want to always add everything but adding each file manually everytime is tedious. That is where a
`.gitignore` is useful. Here, you can tell git what files and folders not to track in plain text. Edit it using a text 
editor by running something like `nano ./.gitignore` for nano, `code ./.gitignore` for VS Code, or `vim ./.gitignore`
for vim.
Format is below:
```gitignore
#This is a comment

#This is a folder you want to ignore
/folder 

#This is a file you want to ignore
file.ext

#You want to ignore all files with a certain extention at the root
*.ext

#You want to ignore all files with a certain extention in the project
**/*.ext
```
Now, running `git add *` will ignore anything that's in the .gitignore file

### Committing Changes
When you've hit a milestone or make a significant change, run `git commit -m "commit-message"`. Think of a commit as a 
snapshot of your project at that specific time. 

### Pushing changes and GitHub

When collaborating with other developers, a central location in the cloud to store files is needed. This is where GitHub
comes in. Open an account and create a repository. Upon creating one, GitHub will show you commands you need to run to 
upload your project to their servers. Once there, you can control who has access to the project in the settings tab. 
The "Issues" tab provides a way to track issues, "Actions" provides CI/CD, "Wiki" provides a way to document your project
and "Pull Requests" provides a way to manage contributions. More on that later. Running `git fetch` in your repository 
after it's been hooked up to GitHub will fetch the latest changes while leaving the uncommitted changes on your system 
intact. `git push` will push any changes you've made to GitHub.

### Cloning Repositories

To download someone else's code, you need to clone it. to clone a repo, run `git clone https://github.com/user/project.git`
Running this will create a new folder at ./project with that project's code

### Branches
Sometimes, developers might want to experiment with changes not knowing if they want to keep them. Branches are ideal 
for this. To create a new branch, run `git checkout -b <branch>` Now, any changes that you make will be committed to this
new branch. Pushing the repo to GitHub will also add the new branch. If you want to accept these changes, going to the
will now show a yellow banner at the top asking you to open a "pull request." Opening onw will allow you to merge the 
request.

### Forks
In the upper right of your repository, there's a button that says "fork". A fork is simply a carbon copy of your 
repository at the time it was clicked that behaves like a branch. You can make changes to it like a normal git repo that
you own but at the top, like a branch, you can merge it back into the master repo via a pull request.

### Collaborating
Git's entire purpose is allowing developers to collaborate. Before we jump in, a few rules to remember
1. Keep the main branch "clean"
   1. It should at least compile even if behavior isn't perfect
2. Don't be afraid to commit and push too much. Commit and push daily, at a minimum when you're making changes
3. Coordinate with your team
   1. 2 users editing the same file and then committing it will result in a "Merge Conflict". in the best case, neither 
   user edited the same lines as the other and both changes can be accepted. Worst case, you're using a language like 
   LabView where merge conflicts can't be resolved you have to throw out one developer's entire work. Either way 
   resolving a merge conflict requires going through code line-by-line 
   and is time-consuming.
   2. Don't have 2 people edit the same file for the reason above. Let's take an FRC example of good coordination:
      1. Clark is working on the LEDs
      2. Alex is working on the climber
      3. Phil is working on the drivetrain
   3. None of them would work on the same files

There are 2 models for collaboration the first is when you trust those working on your code (internal project) and the
second when you don't (large open source project). If you trust your team give them access then, simply have everyone 
clone, and branch the repo for themselves. Let them merge their pull requests once everyone is finished If you don't 
trust your team, require them to fork the repo and work that way. Appoint a "Git Master" to review pull requests and 
merge them appropriately.

## Git in your IDE
Jetbrains has git build into their IDEs. All you have to do is sign in and click on the "VCS" menu in the upper left. 
This menu has everything we just went over as a button except for adding and committing files. That is handled by the 
"Commit" tab under your "Project" tab on the left.

## Git for other uses
Git is the best option for collaboration with any text based files. Your team's website is likely written in HTML, CSS, 
and JS. Even though this is likely handled by your outreach and recruiting team instead of PEP, git would be an ideal 
solution. If your documents presentations and sheets are handled as LaTeX, odp, csv or similar formats, git would also 
work here, although I would recommend moving to Google Workspace for these applications as it allows for real-time as 
opposed to asynchronous collaboration.