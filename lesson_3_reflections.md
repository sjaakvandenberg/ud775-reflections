<!---
# lesson_3_reflections.md
# https://www.udacity.com/course/how-to-use-git-and-github--ud775
# Lesson 3: Using GitHub to Collaborate
#
# In this lesson, you’ll get practice using GitHub or other remote
# repositories to share your changes with others and collaborate on
# multi-developer projects. You’ll learn how to make and review a pull
# request on GitHub. Finally, you’ll get practice by collaborating with
# other Udacity students to write a create-your-own-adventure story.
#
# Sjaak van den Berg
# @svdb
-->

    $ git create ud775-reflections

# When would you want to use a remote repository rather than keeping all your work local?

    $ git push origin master
    $ git pull origin master

# Updated Concept Map

                                  ┌─────┐    ┌────────┐
                                  │ Git │ ~▷ │ GitHub │
                                  └─────┘    └────────┘
                                     △
                                     ~
    ╭────────╮    ╭───────╮    ╱▔▔▔▔▔▔▔▔▔▔╲    ╭────────╮
    │ remote │ ◁# │ clone │ #▷ ▏repository▕ ◁~ │ commit │
    ╰────────╯    ╰───────╯    ╲▁▁▁▁▁▁▁▁▁▁╱    ╰────────╯
        △                            △           △
        #                            @           #
        #       ╭──────╮         ╭────────╮  ╭───────╮
        ####### │ pull │ ######▷ │ branch │  │ merge │
        #       ╰──────╯     #   ╰────────╯  ╰───────╯
        #       ╭──────╮     #
        ####### │ push │ #####   Symbols
                ╰──────╯         -------
                                 ◁# operates on
                                 ◁- type-of
                                 ◁~ part-of
                                 ◁@ refers-to

# Why might you want to always pull changes manually rather than having Git automatically stay up-to-date with your remote repository?

This way you can make corrections when changes are pulled in that break program functionality.

# Describe the differences between forks, clones, and branches. When would you use one instead of another?

Branches happen on a single repository.

Cloning involves taking an existing repository and making one just like it. The original repository could either be remote, or you could even clone a local repository into another spot on your computer.

Forking is only used within the context of GitHub, taking an existing GitHub repository and making a copy of it, whereas clone works on any two repositories.

     Branch                          Clone
    ┌────────────────────────────┐  ┌────────────────────────────┐
    │local                       │  │local                       │
    │         O - O - O          │  │┌───────────┐  ┌───────────┐│
    │              ╲             │  ││ O - O - O │  │ O - O - O ││
    │               O            │  │└───────────┘  └───────────┘│
    └────────────────────────────┘  └────────────────────────────┘
     Fork                            Clone
    ┌────────────────────────────┐  ┌────────────────────────────┐
    │github                      │  │github         local        │
    │┌───────────┐  ┌───────────┐│  │┌───────────┐  ┌───────────┐│
    ││ O - O - O │  │ O - O - O ││  ││ O - O - O │  │ O - O - O ││
    │└───────────┘  └───────────┘│  │└───────────┘  └───────────┘│
    └────────────────────────────┘  └────────────────────────────┘

# Conflicting Collaboration

    ┌────────────────────────────┐  ┌────────────────────────────┐
    │local       b3c ┐           │  │GitHub      df6 ┐           │
    │        ac5 ┐   │           │  │        ac5 ┐   │           │
    │            O - O           │  │            O - O           │
    │                            │  │                            │
    └────────────────────────────┘  └────────────────────────────┘

# A Chili Conflict

Before `git fetch`

    ┌─local──────────────────────┐  ┌─GitHub─────────────────────┐
    │                            │  │                            │
    │                            │  │                            │
    │       chili  +spice        │  │      chili  -cumin         │
    │         O ----- O          │  │        O ----- O           │
    │      origin/  master       │  │              master        │
    │      master                │  │                            │
    │                            │  │                            │
    └────────────────────────────┘  └────────────────────────────┘

`git log origin/master`: chili recipe
`git status`: local branch ahead of origin/master by 1 commit

After `git fetch`

    ┌─local──────────────────────┐  ┌─GitHub─────────────────────┐
    │         origin/master      │  │                            │
    │             O              │  │                            │
    │            ╱ -cumin        │  │      chili  -cumin         │
    │     chili O                │  │        O ----- O           │
    │            ╲ +spice        │  │              master        │
    │             O              │  │                            │
    │           master           │  │                            │
    └────────────────────────────┘  └────────────────────────────┘

`git log origin/master`: chili recipe, -cumin
`git status`: local branch out of sync with origin/master

    Your branch and 'origin/master' have diverged,
    and have 1 and 1 different commit each, respectively.

    $ git merge master origin/master
    $ atom chili-recipe.txt # resolve conflicts
    $ git add chili-recipe.txt
    $ git commit -m "Merge remote-tracking branch 'origin/master'"

As an equivalent for `git fetch` and `git merge`, you can also run `git pull origin master`, which combines the two commands into one.

# Fast Forward Merges

                      Not:              Actual result:

       a ┐  b ┐               b ┐              ab ┐
    O -- O -- O       O -- O -- O       O -- O -- O
                            ╲    ╲
                              --- O
    $ git merge a b             a ┘

When you merging a into b, when a can be reached from b, instead of creating a new commit, we move the ancestor's label to the tip of the branch.

Other examples of fast forward merges:

           O
          ╱ ╲
    1 -- 2   4 -- 5      1 -- 2 -- 3 -- 4
          ╲ ╱   b ┘         a ┘       b ┘
           3
         a ┘

Not fast forward merges, since a can't be reached from b:

         a ┐                  a ┐
           O               O -- O -- O
          ╱               ╱    ╱
    1 -- 2               1 -- 2 -- 3
          ╲                      b ┘
           3
         b ┘

# What is the benefit of having a copy of the last known state of the remote stored locally?

You can incorporate the latest changes in your own work, and benefit from updates and bugfixes.

# Adding A Feature To A Remote Repository

    $ git checkout -b change
    $ git commit -am "Make change"

    ┌─local──────────────────────┐  ┌─GitHub─────────────────────┐
    │                 change     │  │                            │
    │                   O        │  │                            │
    │                 ╱          │  │                            │
    │     O -- O -- O            │  │     O -- O -- O            │
    │             master         │  │             master         │
    │                            │  │                            │
    └────────────────────────────┘  └────────────────────────────┘

    $ git push origin change

    ┌─local──────────────────────┐  ┌─GitHub─────────────────────┐
    │                 change     │  │                 change     │
    │                   O        │  │                   O        │
    │                 ╱          │  │                 ╱          │
    │     O -- O -- O            │  │     O -- O -- O            │
    │             master         │  │             master         │
    │                            │  │                            │
    └────────────────────────────┘  └────────────────────────────┘

    Pull Request

    ┌─local──────────────────────┐  ┌─GitHub─────────────────────┐
    │                 change     │  │                 change     │
    │                   O        │  │                   O        │
    │                 ╱          │  │                 ╱   ╲      │
    │     O -- O -- O            │  │     O -- O -- O ----- O    │
    │             master         │  │                     master │
    │                            │  │                            │
    └────────────────────────────┘  └────────────────────────────┘

# What Gets Changed?

                              local     local     local     GitHub
                              working   staging   master    master
                              dir       area      branch    branch

    edit and save README.md   ✓         ×         ×         ×
    git add README.md         ×         ✓         ×         ×
    git commit                ×         ×         ✓         ×
    git pull origin master    ✓         ✓         ✓         ×
    git push origin master    ×         ×         ×         ✓
    merge alt pull request    ×         ×         ×         ✓

# How would you collaborate without using Git or GitHub? What would be easier, and what would be harder?

Without Git or GitHub, you can collaborate using Dropbox or Google Docs or SVN or some other type of versioning system or by simply emailing files back and forth. For most, an online connection to perform work is needed, and it's slower and doesn't have features such as the pull request. Using a Git or Mercurial based system is a lot easier.

# Updated Concept Map

                                  ╭──────╮
                     ------------ │ fork │ ~~~~~~~
                     -            ╰──────╯       ~
                     ▽          #                ▽
                 ╭───────╮    #   ┌─────┐    ┌────────┐
                 │ clone │   #    │ Git │ ~▷ │ GitHub │ ◁~~~~~~~
                 ╰───────╯  #     └─────┘    └────────┘        ~
               #          #          △                         ~
             ▷              △        ~                         ~
    ╭────────╮                 ╱▔▔▔▔▔▔▔▔▔▔╲    ╭────────╮   ╭────╮
    │ remote │ @@@@@@@@@@@@@@▷ ▏repository▕ ◁~ │ commit │   │ PR │
    ╰────────╯                 ╲▁▁▁▁▁▁▁▁▁▁╱    ╰────────╯   ╰────╯
        △                            △           △       ◁     #
        #                            @           #     ~       #
        #       ╭──────╮         ╭────────╮  ╭───────╮         #
        ####### │ push │ ######▷ │ branch │  │ merge │         #
        #       ╰──────╯     #   ╰────────╯  ╰───────╯         #
        #       ╭──────╮     #           △       -             #
        ####### │ pull │ #####           #######################
        #       ╰──────╯ ◁---#--------------------
        #           △        #
        #           ~        #   Symbols
        #       ╭───────╮    #   --------------
        ####### │ fetch │ ####   ◁# operates on
                ╰───────╯        ◁- type-of
                                 ◁~ part-of
                                 ◁@ refers-to

# When would you want to make changes in a separate branch rather than directly in master? What benefits does each approach have?

Creating a separate branch for your changes keeps your changes organized and easy to review. It won't break the master branch, so you can experiment with the changes before you add them to the master branch. It also makes collaboration easier, which each collaborator making separate branches for their contributions.

    $ git pull upstream master
    $ git checkout forest
    $ git merge master forest
    $ git push origin forest
    $ git checkout master
    $ git push
