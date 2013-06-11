git-hooks-jira
==============
  
## Description
  
  When you use JIRA, do you want to input JIRA-ticket in your commit message. Therefore, in the future, when you look back to code, you can easily know why you or your team member changed this code. In addtionally, by using Agile development, you also need to log time to let project management team knows what are doing now? How about this ticket? They can know how the project goes.
  But sometimes, you will forget to log your worked time. How to solve this kind of problem? Here is the solution, Using [git hooks](http://git-scm.com/book/en/Customizing-Git-Git-Hooks) and [JIRA rest api](https://docs.atlassian.com/jira/REST/latest/) to automatically update log time according to JIRA ticket number.

## Environment
  
 `Ruby 1.9.2` and `Ruby 1.9.3`

## How to use

`git clone https://github.com/hebinbin/git-hooks-jira.git` to your local pc.

Set you JIRA username and password in git config

* `git config --global jira.username hogehoge`
     
* `git config --global jira.password hogehoge`

Go to your project, use `ls -al` command to check whether you have `.git` folder or not. If you do not have, please `git init` to create a new `.git` folder.

`cd .git/hooks` , move `commit-msg` `post-checkout` `post-commit` `pre-commit` `prepare-commit-msg` from git-hooks-jira folder to current folder.

Change the property of files.
  
* `sudo chmod +x commit-msg`
 
* `sudo chmod +x post-checkout`

* `sudo chmod +x post-commit`
     
* `sudo chmod +x pre-commit`
     
* `sudo chmod +x prepare-commit-msg`

Go to `post-commit` file, change site link to your JIRA address.

Work pattern: (Using pull request)
  
1) You need to checkout a new branch. Please put ticket number in the branch like `pr-WEB-12345`.
 
   `git checkout -b pr-WEB-12345 origin/remote-branch`

after that git will read `post-checkout` hooks to change status of WEB-12345 from `Start progress` to `In progress`

2) You begin to change the code. When you commit, please input your worked time in your commit message.

   `git add something`
     
   `git commit -m "#0.3h fixed a bug about display issue"`

the commit message will automatically become `Ticket #WEB-12345 #0.3h fixed a bug about display issue` and read JIRA api to update ticket.





