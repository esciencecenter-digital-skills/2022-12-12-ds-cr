![](https://i.imgur.com/iywjz8s.png)


# Collaborative Document: Good Practices in Research Software Development (Code Refinery)

2022-12-12-ds-cr day 2

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
| Time  | Topic                             |
|------:|:----------------------------------|
| 9:00  | Welcome and icebreaker            |
| 9:15  | Workshop Introduction             |
| 9:30  | Collaboration with Git and GitHub |
| 10:15 | Coffee break                      |
| 10:30 | Collaboration with Git and GitHub |
| 11:30 | Coffee break                      |
| 11:45 | Collaboration with Git and GitHub |
| 12:45 | Wrap-up                           |
| 13:00 | END                               |


## 🔧 Exercises
### Exercise: Working as a project collaborator (in breakout rooms)

- Log into Github and create a new repository
- Make the repository public
- clone it to your desktop
- add some code
- push the changes to the repository
- Add one person as a collaborator (settings -> Manage Access). Make sure everyone in the group has a collaborator.
- Create an issue in the repo where you are a collaborator
- Clone that repo
- make changes on a new branch
- push the changes
- submit a Pull Request
- wait for approval
- At the same time review a collaborators Pull Request
- (Optionally) Learn about [protecting branches](https://docs.github.com/en/github/administering-a-repository/about-protected-branches) and try it out.

### Exercise: Working as an external contributor (in breakout rooms)
- Remove your group member(s) as collaborators from your repository
- Fork another group members repo (Repository page, top right corner)
- Create an issue on the original repository
- Clone your forked repo to your computer
- Make some changes, use a somewhat real-world example so it makes sense to review it (but don't overdo it).
- Push it to your fork
- make a pull request from your fork to the main repository mentioning the issue
- Consider turning your Pull Request into a draft Pull Request.
- let your code be reviewed by tagging the repo owner using (@Username)
- At the same time review Pull Request using comments on individual lines. Try to act as if it was a real peer review as much as possible.
- Accept or reject the Pull Request
- (Optionally) learn about [merge conflicts](https://www.atlassian.com/git/tutorials/using-branches/merge-conflicts) and try it out in your collaboration.

## 🧠 Collaborative Notes

### Workshop introduction
Summary of the entire workshop: how to write good/better code?
- You need to prioritize
- Software engineering tools can speed up development on the long run

Check your ssh connection:
```bash=
ssh -T git@github.com
```


### Collaboration with Git and Github
* How can we collaborate with others within one repository?
* How can we collaborate with people who we might not know yet?
* What is a fork?
* What is a pull request or merge request?
* What is code review?


#### Working collaboratively on Github
Create a new repository on Github.
It is nice to choose a pre-defined gitignore file, e.g. one for Python.
Licensing is important, it describes if/how others can you use code. The default at the eScience Center is Apache 2.0, but discuss in your department what you should use.

Organize the work that needs to be done by creating issues You can assign people to issues.

Clone the repository to your computer:
```bash=
git clone git@github.com:<your username>/<your repository name>.git
```

If you selected a license and gitignore file on Github, you should see a LICENSE and .gitignore file in the repository.
The gitignore file is a hidden file, so you need `ls -a` to see it.

Create a new file called add.py and write a Python function that adds two numbers:
```bash=
nano add.py
```

We are still working on the Git main branch. Typically this is a bad idea! When you're collaborating, you might want to let someone else check your code first, before applying it.
We do this by creating a new branch for our change, and merging that with the main branch after checking the code.

Make a new branch called `addition`:
```bash=
git checkout -b addition
```

Add the new file to git:
```bash=
git add add.py
git commit -m "Write an addition function"
git status
```
Note that git status also shows which branch you are on, in our case `addition`. `git branch` shows all local branches.

We now want to push our changes to Github, but the addition branch does not exist yet on Github. We push and create the branch with one command:
```bash=
git push --set-upstream origin addition
```
A shortcut for `--set-upstream` is `-u`.
Once you have used the `-u` option, you can simply do `git push` in the future. You have to repeat the command with the `-u` option once for every new branch you make on your computer.

When you make a new branch, you typically make sure you are on the main branch first. This is because the new branch will be a copy of the current branch.

Current situation on Github:
- a main branch with only the gitignore and license file
- an addition branch that also includes the add.py file

Now we want to get an overview of our changes in the addition branch, and let our collaborator review them.

On the Github webpage, it might already suggest that you want to create a `pull request`. You can also click the pull requests tab in the menu above the code.
Then you select the select the main branch as the base branch (where your changes will be merged into) and the addition branch as comparison branch (where the changes are coming from).

In the pull request, often shortened to PR, you can give a description of your changes. Maybe even include a bit of code showing how someone can test the new code.
You can also link to issues, or even automatically close them with when the PR is merged with seomthing like `Closes #1`.

You can assign reviewers to pull requests. Those people will get a notification requesting their review.

Everyone has their own style of reviewing. We think the most important is to stay nice to each other. Reviewing can quickly become a very toxic thing otherwise.

When reviewing you can comment on specific pieces of code and even make suggestions that can automatically be committed.

If needed you can edit the comments in the PR. The first comment is typically used as the description, so it is often updated with the most up-to-date information.
Note: you _can_ edit other people's comments, but don't do that.

Finally, you can click "Merge Pull Request". Typically a PR is merged by the person that opened it. Github then suggests you can remove the branch that we made for this change. Note: only the remote branch, on Github, is deleted.

Locally, we can no longer pull the addition branch since it was deleted
```bash=
git pull # will give an error
```
We can go back to the main branch. Git will already tell you there are changes you don't have locally yet.
```bash=
git checkout main
git pull
```

The local addition branch is not automatically deleted. To do this, run:
```bash=
git branch -d addition
```

The network tab (found under Insights -> Network) on Github shows the different branches and commits in a nice graph.

When you are working in a branch for a while, there may be some changes to main as well that you would want to merge into your branch. You can do this by running `git pull origin main` while within your branch.

#### Working with external collaborators
We will now repeat this exercise, but in a slightly different situation: what if you don't have access to the repository with the code you want to change?

Instead of cloning the repository you want to work on, you can create a remote version in your own Github account with the fork button on Github. This will copy the repository to your account.

Now you can make some changes. Doing this in the main branch is not much of a problem now, because it is the main branch of your own copy of the repository. It doesn't change the main branch of the original repository.

When you create a pull request, you can choose the original repository as a base, and it will open the pull request there instead of in your own repository.

It might be that the same file was changed by multiple people. Then you may get a merge conflict: Git doesn't know how to combine the different changes.
The Github webpage has an interface to inspect and fix the merge conflicts. Typically the person that opened the PR fixes the merge conflict. Git adds some text with <<<, ===, and >>> symbols wherever it found a merge conflict.
The changes will be committed to your branch.

### Key Points
* Git and Github are superpowerful, not just for version control, but as tools for collaborative development
* Do code reviews and be constructive in them!
* Use centralized flow for internal collaborations
* Use distributed flow for external collaborations

## 📚 Resources
* [eScience Center call for proposals](https://www.esciencecenter.nl/calls-for-proposals)
* [Upcoming workshops](https://www.esciencecenter.nl/digital-skills)
* [NL-RSE community](https://www.nl-rse.org)
* [Git commands cheat sheet](https://education.github.com/git-cheat-sheet-education.pdf)
* [Simple peer review real-life example](https://github.com/carpentries-incubator/deep-learning-intro/pull/269)