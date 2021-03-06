Version Control Collaboratively

----

[Back To Local Version
Control](http://github.com/thehackerwithin/UofCSCBC2012/tree/master/3a-VersionControlLocal/)
- [Forward To
Debugging](http://github.com/thehackerwithin/UofCSCBC2012/tree/master/4-Debugging/)

----

**Presented By : Anthony Scopatz**
**Developed By : Katy Huff**

## github.com?

GitHub is a site where many people store their open (and closed) source
code repositories. It provides tools for browsing, collaborating on and
documenting code. Your home institution may have a repository hosting system
of it's own. To find out, ask your system administrator.
GitHub, much like other forge hosting services 
( [launchpad](https://launchpad.net),
[bitbucket](https://bitbucket.org), [googlecode](http://code.google.com), 
[sourceforge](http://sourceforge.net) etc.)
provides :

-   landing page support [my research is at 
    cyclus.github.com](http://cyclus.github.com)
-   wiki support
-   network graphs and time histories of commits
-   code browser with syntax highlighting
-   issue (ticket) tracking
-   user downloads
-   varying permissions for various groups of users
-   commit triggered mailing lists
-   other service hooks (twitter, etc.)

## github pasword 

Setting up github at first requires a github user name and password. 
Please take a moment to [create a free one](https://github.com/signup/free)
(if you want to start paying, you can add that to your account some 
other day). 

## github ssh keys

It will help you to set up automatic authorization, so that github can handshake
with your computer (in this case, your virtual machine).
There are [some setup instructions](http://help.github.com/set-up-git-redirect)  
on the website, but I'll do this along with you at the front of the room as 
well. 

    $ cd ~/.ssh

It will likely say "no such file or directory."

    $ ssh-keygen -t rsa -C "your_email@youremail.com"
    Generating public/private rsa key pair.
    Enter file in which to save the key (/home/thw/.ssh/id_rsa):  <press enter>

The path that it provides will be to this home directory. This is okay. **Press 
enter.** You may enter a passphrase. You'll see something like this :

    Created directory '/home/thw/.ssh'.
    Enter passphrase (empty for no passphrase): 
    Enter same passphrase again: 
    Your identification has been saved in /home/thw/.ssh/id_rsa.
    Your public key has been saved in /home/thw/.ssh/id_rsa.pub.
    The key fingerprint is:
    09:06:c6:0f:24:b7:84:ef:22:74:de:95:f0:99:64:5d your_email@youremail.com
    The key's randomart image is:
    +--[ RSA 2048]----+
    |  .+*   . .E     |
    |  .=o+ o .       |
    |   ..oB +        |
    | . ....B .       |
    |. o.. . S        |
    |. ....           |
    | . .             |
    |                 |
    |                 |
    +-----------------+

## git config : Configuring your git environment

Once you've set up your rsa keys, you need to tell github who you are.
Crack open a terminal.

    $ git config --global user.name "Firstname Lastname"
    $ git config --global user.email "your_email@youremail.com"

Unless your name is Firstname Lastname, please don't copy the above
lines verbatim. Make the appropriate substitutions.

If you did this properly, you'll have a file in your home **(\~)**
directory that's called **.gitconfig** . It's contents should look like
:

    [user]
          name = Katy Huff
          email = southside@gmail.com

This configuration step allows github to properly credit the authorship
of changes you make in your repository. For projects with numerous
authors, this is essential.

Another configuration step for some will be to set their favorite text
editor as git's text editor of choice. This is optional, since vi is
usually the default, but can be done with the following command (if you
like **nano** for example):

    $ git config --global core.editor nano

## git remote : Steps for Forking a Repository

A key step to interacting with an online repository that you have forked
is adding the original as a remote repository. By adding the remote
repository, you inform git of a new option for fetching updates and
pushing commits.

The **git remote** command allows you to add, name, rename, list, and
delete repositories such as the original one **upstream** from your
fork, others that may be **parallel** to your fork, and so on.

### Exercise : Fork Our GitHub Repository

While you probably already have a copy of the UofCSCBC2012 repository,
GitHub doesn't know about it yet. You'll need to tell github you want to
have an official fork of this repository.

Step 1 : Go to our 
[repository](https://github.com/thehackerwithin/UofCSCBC2012/) from your browser, and
click on the Fork button. Choose to fork it to your username rather than
any organizations.

Step 2 : Clone it. From your terminal :

    $ git clone git@github.com:username/UofCSCBC2012.git
    $ cd UofCSCBC2012

Step 3 :

    $ git remote add upstream git://github.com/thehackerwithin/UofCSCBC2012.git
    $ git remote -v
    origin  git@github.com:username/UofCSCBC2012.git (fetch)
    origin  git@github.com:username/UofCSCBC2012.git (push)
    upstream        git://github.com/thehackerwithin/UofCSCBC2012.git (fetch)
    upstream        git://github.com/thehackerwithin/UofCSCBC2012.git (push)

All repositories that are clones begin with a remote called origin.

## git fetch : Fetching the contents of a remote

Now that you have alerted your repository to the presence of others, it
is able to pull in updates from those repositories. In this case, if you
want your master branch to track updates in the original UofCSCBC2012
repository, you simply **git fetch** that repository into the master
branch of your current repository.

The fetch command alone merely pulls down information recent changes
from the original master (upstream) repository. By itself, the fetch
command does not change your local working copy. To update your local
working copy to include recent changes in the original (upstream)
repository, it is necessary to also merge.

## git merge : Merging the contents of a remote

To incorporate upstream changes from the original master repository (in
this case thehackerwithin/UofCSCBC2012) into your local working copy, you
must both fetch and merge. The process of merging may result in
conflicts, so pay attention. This is where version control is both at
its most powerful and its most complicated.

### Exercise : Fetch and Merge the Contents of Our GitHub Repository

Step 1 : Fetch the recent remote repository history

    $ git fetch upstream

Step 2 : Make certain you are in the master branch and merge the
upstreeam master branch into your master branch

    $ git checkout master
    $ git merge upstream/master

Step 3 : Check out what happened by browsing the directory.

## git pull : Pull = Fetch + Merge

The command **git pull** is the same as executing **git fetch** followed
by **git merge**. Though it is not recommened for cases in which there
are many branches to consider, the pull command is shorter and simpler
than fetching and merging as it automates the branch matching.
Specificially, to perform the same task as we did in the previous
exercise, the pull command would be :

    $ git pull upstream
    Already up-to-date.

When there have been remote changes, the pull will apply those changes
to your local branch, unless there are conflicts with your local
changes.

## git push : Sending Your Commits to Remote Repositories

The **git push** command pushes commits in a local working copy to a
remote repository. The syntax is git push [remote] [local branch].
Before pushing, a developer should always pull (or fetch + merge), so
that there is an opportunity to resolve conflicts before pushing to the
remote.

We'll talk about conflicts later, but first, since we have no conflicts
and are up to date, we can make a minor change and send our changes to
your fork, the "origin."

    $ git push origin master

If you have permission to push to the upstream repository, sending
commits to that remote is exactly analagous.

    $ git push upstream master

In the case of the UofCSCBC2012 code, new developer accounts will not allow
this push to succeed. You're welcome to try it though.

## git merge : Conflicts

This is the trickiest part of version control, so let's take it very
carefully.

In the UofCSCBC2012 code, you'll find a file called Readme.md. This is a
standard documentation file that appears rendered on the landing page
for the repository in github. To see the rendered version, visit your
fork on github,
[https://github.com/username/UofCSCBC2012/](https://github.com/username/UofCSCBC2012/)
.

For illustration, let's imagine that, suddenly, each of the developers
on the UofCSCBC2012 code would like to welcome visitors in a language other
than English. Since we're all from so many different places and speak
so many languages, there will certainly be disagreements about what to
say instead of "Welcome."

I, for example, am from Texas, so I'll push (to the upstream repository)
my own version of Welcome on line 2 of Readme.md.

You may speak another language, however, and may want to replace the 
english word Welcome with an equivalent word that you prefer (willkommen, 
bienvenido, benvenuti, etc.).

You'll want to start a new branch for development. It's a good
convention to think of your master branch as the "production branch,"
typically by keeping that branch clean of your local edits until they
are ready for release. Developers typically use the master branch of
their local fork to track other developers changes in the remote
repository until their own local development branch changes are ready
for production.

### Exercise : Experience a Conflict

Step 1 : Make a new branch, edit the readme file in that branch, and
commit your changes.

    $ git branch development
    $ git checkout development
    Switched to branch 'development'
    $ gedit Readme.md &
    <edit the readme file and exit gedit>
    $ git commit -am "Changed the welcome message to ... "

Step 2 : Mirror the remote upstream repository in your master branch by
pulling down my changes

    $ git checkout master
    Switched to branch 'master'
    $ git fetch upstream
    $ git merge upstream/master
    Updating 43844ea..3b36a87
    Fast-forward
     README.rst |   2 +-
     1 files changed, 1 insertions(+), 1 deletions(-)

Step 3 : You want to push it to the internet eventually, so you pull
updates from the upstream repository, but will experience a conflict.

    $ git merge development
    Auto-merging Readme.md
    CONFLICT (content): Merge conflict in Readme.md
    Automatic merge failed; fix conflicts and then commit the result.

## git resolve : Resolving Conflicts

Now what?

Git has paused the merge. You can see this with the **git status**
command.

    # On branch master
    # Unmerged paths:
    #   (use "git add/rm <file>..." as appropriate to mark resolution)
    #
    #       unmerged:      Readme.md
    #
    no changes added to commit (use "git add" and/or "git commit -a")

The only thing that has changed is the Readme.md file. Opening it,
you'll see something like this at the beginning of the file.

    =====================
    <<<<<<< HEAD
    Howdy
    =======
    Willkommen
    >>>>>>> development
    =====================

The intent is for you to edit the file, knowing now that I wanted the
Welcome to say Howdy. If you want it to say Willkommen, you should
delete the other lines. However, if you want to be inclusive, you may
want to change it to read Howdy and Willkommen. Decisions such as this
one must be made by a human, and why conflict resolution is not handled
more automatically by the version control system.

    =====================
    Howdy and Willkommen
    =====================

This results in a status To alert git that you have made appropriate
alterations,

    $ git add Readme.md
    $ git commit
    Merge branch 'development'

    Conflicts:
      Readme.md
    #
    # It looks like you may be committing a MERGE.
    # If this is not correct, please remove the file
    # .git/MERGE_HEAD
    # and try again.
    #
    $ git push origin master
    Counting objects: 10, done.
    Delta compression using up to 2 threads.
    Compressing objects: 100% (6/6), done.
    Writing objects: 100% (6/6), 762 bytes, done.
    Total 6 (delta 2), reused 0 (delta 0)
    To git@github.com:username/UofCSCBC2012.git
