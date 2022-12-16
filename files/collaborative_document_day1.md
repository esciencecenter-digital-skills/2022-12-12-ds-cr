![](https://i.imgur.com/iywjz8s.png)


# Collaborative Document: Good Practices in Research Software Development (Code Refinery)

2022-12-12-ds-cr day 1

Welcome to The Workshop Collaborative Document.

This Document is synchronized as you type, so that everyone viewing this page sees the same text. This allows you to collaborate seamlessly on documents.

----------------------------------------------------------------------------


## 👮Code of Conduct

Participants are expected to follow these guidelines:
* Use welcoming and inclusive language.
* Be respectful of different viewpoints and experiences.
* Gracefully accept constructive criticism.
* Focus on what is best for the community.
* Show courtesy and respect towards other community members.

## 🎓 Certificate of attendance

If you attend the full workshop you can request a certificate of attendance by emailing to training@esciencecenter.nl .

## ⚖️ License

All content is publicly available under the Creative Commons Attribution License: [creativecommons.org/licenses/by/4.0/](https://creativecommons.org/licenses/by/4.0/).

## 🙋Getting help

To ask a question, raise your hand in zoom. Click on the icon labeled "Reactions" in the toolbar on the bottom center of your screen,
then click the button 'Raise Hand ✋'. For urgent questions, just unmute and speak up!

You can also ask questions or type 'I need help' in the chat window and helpers will try to help you.
Please note it is not necessary to monitor the chat - the helpers will make sure that relevant questions are addressed in a plenary way.
(By the way, off-topic questions will still be answered in the chat)


## 🖥 Workshop website

[link](https://esciencecenter-digital-skills.github.io/2022-12-12-ds-cr/)

🛠 Setup

[link](https://esciencecenter-digital-skills.github.io/2022-12-12-ds-cr#setup)

## 👩‍🏫👩‍💻🎓 Instructors

Barbara Vreede, Sven van der Burg, Leon Oostrum

## 🧑‍🙋 Helpers

Luisa Orozco, Dani Bodor


## 🗓️ Agenda
| Time | Topic |
|--:|:---|
| 9:00 | 	Welcome and icebreaker |
| 9:15 | Introduction to version control with Git |
| 10:15 | Coffee break |
| 10:30 | Introduction to version control with Git |
| 11:30 | Coffee break |
| 11:45 | Introduction to version control with Git |
| 12:45 | Wrap-up |
| 13:00 | END |


## 🔧 Exercises

### Exercise 1

#### part 1
Along with tracking information about planets (the project we have already created), Dracula would also like to track information about moons. Despite Wolfman’s concerns, Dracula creates a moons project inside his planets project with the following sequence of commands:
```
$ cd ~/Desktop   # return to Desktop directory
$ cd planets     # go into planets directory, which is already a Git repository
$ ls -a          # ensure the .git subdirectory is still present in the planets directory
$ mkdir moons    # make a subdirectory planets/moons
$ cd moons       # go into moons subdirectory
$ git init       # make the moons subdirectory a Git repository
$ ls -a          # ensure the .git subdirectory is present indicating we have created a new Git repository
```
Is the git init command, run inside the moons subdirectory, required for tracking files stored in the moons subdirectory?

#### part 2
Wolfman explains to Dracula how a nested repository is redundant and may cause confusion down the road. Dracula would like to remove the nested repository. How can Dracula undo his last git init in the moons subdirectory?

### Exercise 2: Tracking changes exercise
Exercise in breakout rooms. Write down your (joint) answers to the next 3 questions in the collaborative notebook.

#### 0
Which of the following commit messages would be most appropriate for the last commit made to mars.txt?

“Changes”
“Added line ‘But the Mummy will appreciate the lack of humidity’ to mars.txt”
“Discuss effects of Mars’ climate on the Mummy”
#### 1. Which command(s) below would save the changes of myfile.txt to my local Git repository?

1. git commit -m "my recent changes"
2. git init myfile.txt
   git commit -m "my recent changes"
3. git add myfile.txt
   git commit -m "my recent changes"
4. git commit -m myfile.txt "my recent changes"

#### 2. Committing Multiple Files
The staging area can hold changes from any number of files that you want to commit as a single snapshot.

Add some text to ``mars.txt`` noting your decision to consider Venus as a base
Create a new file ``venus.txt`` with your initial thoughts about Venus as a base for you and your friends
Add changes from both files to the staging area, and commit those changes.

#### 3. (optional) A new repository
Create a new Git repository on your computer called bio.
Write a three-line biography for yourself in a file called me.txt, commit your changes
Modify one line, add a fourth line
Display the differences between its updated state and its original state.



### Exercise 3: exploring history exercise
Write down your (individual) answers to the next 3 questions in the collaborative notebook.

#### 1. Recovering Older Versions of a File
Jennifer has made changes to the Python script that she has been working on for weeks, and the modifications she made this morning “broke” the script and it no longer runs. She has spent ~ 1hr trying to fix it, with no luck…

Luckily, she has been keeping track of her project’s versions using Git! Which commands below will let her recover the last committed version of her Python script called `data_cruncher.py?`

1. `$ git checkout HEAD`
2. `$ git checkout HEAD data_cruncher.py`
3. `$ git checkout HEAD~1 data_cruncher.py`
4.  ` $ git checkout <unique ID of last commit> data_cruncher.py`
5.  Both 2 and 4

#### 2. Reverting a Commit

Jennifer is collaborating on her Python script with her colleagues and realizes her last commit to the project’s repository contained an error and she wants to undo it. `git revert [erroneous commit ID]` will create a new commit that reverses Jennifer’s erroneous commit. Therefore `git revert` is different to `git checkout [commit ID]` because `git checkout` returns the files within the local repository to a previous state, whereas `git revert` reverses changes committed to the local and project repositories.
Below are the right steps and explanations for Jennifer to use `git revert`, what is the missing command?

1. `________ # Look at the git history of the project to find the commit ID`
2. `Copy the ID (the first few characters of the ID, e.g. 0b1d055).`
3. `git revert [commit ID]`
4. Type in the new commit message.
5. Save and close


#### 3. Understanding Workflow and History

What is the output of the last command in
```
$ cd planets
$ echo "Venus is beautiful and full of love" > venus.txt
$ git add venus.txt
$ echo "Venus is too hot to be suitable as a base" >> venus.txt
$ git commit -m "Comment on Venus as an unsuitable base"
$ git checkout HEAD venus.txt
$ cat venus.txt #this will print the contents of venus.txt to the screen
```
1. Venus is too hot to be suitable as a base
2. Venus is beautiful and full of love
3. Venus is beautiful and full of love
4. Venus is too hot to be suitable as a base
5. Error because you have changed venus.txt without committing the changes


### Exercise 4 (optional) Push vs. Commit

In this lesson, we introduced the `“git push”` command. How is `“git push”` different from `“git commit”`?



## 🧠 Collaborative Notes
Question: how do you work on your project? How do you save results, and how do you backup your projects?
- backup once a month
- manual backups
- git for backups

Why do we use version control?
- Storing separate versions becomes neat and clean; especially important when projects grow bigger.
- It also allows smooth collaboration on software especially.
- It is the standard for sharing code.

Git keeps track of changes. This also allows multiple different changes to be combined into the same document.

Version control is like an unlimited 'undo'.
Version control allows many people to work in parallel.

### let's get to work :)
Open up the terminal of your choice/OS.

Configuring our name and email address for git:
```bash=
git config --global user.name "Your Name"
git config --global user.email "myemail@mydomain.com"
git config --list
```

The last command shows the states of your global configurations. If you want to exit the view, type `q`

Configure line endings:
```bash=
git config --global code.autocrlf input # for mac and linux
git config --global code.autocrlf false # for windows
```
We do this because otherwise differences in line endings will make git think that every line is different, so every line will be seen as a change.

Configure the text editor:
```bash=
git config --global core.editor "nano -w"
```
(The -w flag makes nano wrap your text; if you have long texts, they will be wrapped around instead of generating a very long line.)

Access help:
```bash=
git config -h
```

More help:
[search online :)](https://www.google.com)


### Making a repository
We start with a new directory.

Move to the place where you want to make the directory, and create it there:
```bash=
cd ~/Desktop
mkdir planets
cd planets
```
going out of a directory is done by `cd ..`.
You can find a name of a path by typing its first letters, and then using your [tab] key to autocomplete the name :)

We will now turn the directory into a git repository:
```bash=
git init
```
We have our first git repository 🎉

What is inside it?
```bash=
ls -a
```
The -a flag makes ls show the hidden files, too.
This shows a `.git` directory; that is the content of our version control.
Let's take a peek inside:
```bash=
ls -a .git
```

Git is a local program; it works like this without connection to an online location (like github or gitlab). Using these options in the cloud will amp up its functionality, and we'll get to that!

Git names its first branch `master`. This was common until a few years ago; we now use the name `main` for the default branch. To change the name of our branch, we can use two options:

```bash=
git branch -m main
```
or
```bash=
git checkout -b main
```
the second option can be used also to make any new branch with any name. The first option flags the branch `main` as the initial branch.

To check what branches exist:
```bash=
git branch
```

Make sure you see hints when Git gives them!
```bash=
git config --global status.hints true

```

Check where you are:
```bash=
pwd
```

### Tracking changes
Recording changes in Git works via two commands: `add` and `commit`. Let's see them in action.

We will first start working on a document to track changes in.
We will use Nano to write a document:
```bash=
nano mars.txt
```
This will open Nano in the terminal, you can edit the newly created document here.
Write some text in this document, then save it and exit using [control] + X then type Y to save.

Check that the file exists now:
```bash=
ls
```
this should show the content of the folder.
```bash=
cat mars.txt
```
should show us the content of the file `mars.txt`.

Let's check the status of our repository:
```bash=
git status
```
Git now informs us that `mars.txt` has been changed, but is not tracked. We will add it to start tracking:

```bash=
git add mars.txt
git status
```
The status check gives us an update: `mars.txt` is tracked but changes need to be committed. Let's do this:
```bash=
git commit -m "Start notes on Mars as a base"
```
In `-m ""` we give a message that describes our changes
These messages should be informative; they are what will later help you find specific changes in your history.

Check this history:
```bash=
git log
```
It's good practice to commit changes when you're done with any piece that you're working on. Small commits are better than huge ones!

Git is designed in such a way that changes that are tracked need to be consciously added and committed. You won't accidentally commit things that are not important, or even unwanted.

Note that Git keeps track of files, not directories. If you want to track a directory that is empty, you can add a (hidden, empty) file inside it, like `.gitkeep`.

Let's add some more content
```bash=
nano mars.txt
```
Add some text to this file.

```bash=
git diff
```
shows us the difference between the current state of the repository, and the last committed version.

Whenever we go through a change, you follow this pattern:
```bash=
git add [file]
git commit -m "[commit message]"
```
where [file] is the file name that you want to add to this commit. You can add multiple files, either by writing multiple file names here, or by repeating the `git add` command, if your commit consists of multiple files.
Then in the [commit message] you will describe the change for your history.

![](https://i.imgur.com/7i0LESP.png)

#### Q: What is the purpose of having this add - commit system, why not just have a single process?
You can make decisions about what you include during the `add` part:
- what files do you include in the commit? What files stay out? (e.g. files created by your system)
- what *part* of the file that you changed will be included in the commit?

Then you make the final call to put everything in the staging area into the repository, during the `commit`, and give it a label:
- what will you label your changes?

Checking your changes:
```bash=
git diff
git diff --staged
```

Writing a good commit message is an art.

[![](https://imgs.xkcd.com/comics/git_commit_2x.png)](https://xkcd.com/1296/)

### Committing multiple files
We are making changes in multiple files:

```bash=
nano venus.txt
nano mars.txt
```

Then we add both files to the staging area
```bash=
git add venus.txt mars.txt
```

Now we commit both together:
```bash=
git commit -m "Write plans to start a base on venus"
```

### Looking at our changes

```bash=
git diff HEAD mars.txt
```
will show us the changes between the most recent commit and the current state of the file (uncommitted).

We can also look at the difference between the curent state and any other point in time:

```bash=
git diff HEAD~3 mars.txt
```
for instance shows the changes between now and 3 commits ago.

We can look at a specific commit, too:
```bash=
git show HEAD~3 mars.txt
```
The difference here is what was made in that particular commit.
You can refer to a particular commit using the `~n` where n is the number of commits back from current.

But commits have a hash that allows us to refer to them specifically. you can see them with
```bash=
git log
```
where every commit has a specific ID (the long string of numbers after the word `commit`)
```bash=
git show 11157329359230fhsdf0df9sdg0s0gsdg9sg77sd99sd
```
Or, as a shorter version:
```bash=
git show 1115732
```
(the length does not matter, as long as those characters are unique for commits in your repository)

But now...
How do we get back to this version of our file?

We do this with `checkout`:
```bash=
git checkout HEAD mars.txt
```
this update mars.txt to the latest commit. That removes any uncommitted changes that happened since.

We can even go further back in time:
```bash=
git checkout 1115732 mars.txt
```
this reverts the file back to its state for that commit, BUT it does not automatically commit it. It does add it to the staging area (you can see this by running `git status`). You can commit it, describing why you reverted the change. Or you can go back to your latest commit:

```bash=
git checkout HEAD mars.txt
```

If you forget the file name, you go back in history, in what is called a 'detached head' state:

```bash=
git checkout 1115732
```
Git will warn you! You can go back by checking out the repository branch:
```bash=
git checkout main
```

If we want, we can undo a commit:
```bash=
git revert 1115732

```
This undoes the changes made during this commit; and it will open an editor because this reversion is also a commit in and of itself: your revert will become part of the history, and you need to describe it in a commit message.


### Ignoring files
If, e.g., your script produces certain output files which you don't want to track, they might clutter up your `git status`, or they will confuse you and might accidentally be committed. How do we make sure this doesn't happen?

Let's create some files in a directory
```bash=
mkdir result
touch a.dat b.dat c.dat results/a.dat results/b.dat
```

`git status` now gives us these files as 'untracked'.

But we want to ignore them. We can do this with a file called `.gitignore`.
```bash=
nano .gitignore
```
Make sure you put this file in the root. You can also make it in subfolders, but then the rules of this gitignore file will only apply to the subfolder.
We can add filetypes:
```bash=
*.dat
```
Or entire folders:
```bash=
results/
```
We do want to add this file:
```bash=
git add .gitignore
git commit -m "ignore dat files and results/ folder"
```
You can explicitly add a file that is ignored in the .gitignore file, but you have to flag your add command:
```bash=
git add -f a.dat
```
You can also explicitly give the status of ignored files:
```bash=
git status --ignored
```

### CHECK YOUR SSH:
```bash=
ssh -T git@github.com
```
This should say:
```!
Hi [username]! You've successfully authenticated, but GitHub does not provide shell access.
```
IF NOT! LET US KNOW! Your SSH key pair does not work and needs to be fixed before you can collaborate on GitHub.


### Collaborating on a git repository

Our instructors now exchange the repository by emailing a zip file. This is not the best way to collaborate! Instead, let's learn how to work together with a synchronized 'remote' repository.

Our remote repository will live on GitHub.
We will create an empty repository by logging into github, and then cliking the + icon in the top right corner.

We will name our repository 'planets', leave the defaults, don't create any new documents, but click 'create repository'.

We will go to the section "push an existing repository from the command line", which gives the following code:
```bash=
git remote add origin git@github.com/[username]/[reponame].git
git push -u origin main
```
`origin` is the most often used name for the main remote repository.

The `remote add` command only links the repository online to our local version.
You can check the remote location with:
```bash=
git remote -v
```
Now refresh the page of your github repository. you should now see the files and history of your work done locally!

Here, you can also make edits, by clicking the pencil icon when looking at a file, and then committing the results (scroll to the bottom).

When we want to get these changes into our local repository, we can 'pull' them:

```bash=
git pull
```
Now, locally these changes exist too!

If you didn't use the `-u` flag when pushing the repository (`git push -u origin main`), the remote branch has not been linked; you simply pushed the contents but not defined the remote branch as a 'default' to push to.

You can do so at any time; either with `-u` or:
```bash=
git push --set-upstream origin main
```



## 📚 Resources