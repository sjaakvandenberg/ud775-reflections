<!---
# lesson_2_reflections.md
# https://www.udacity.com/course/how-to-use-git-and-github--ud775
# Lesson 2: Creating and Modifying a Repository
#
# In this lesson, you’ll learn how to create a repository and save versions
# of your project. You’ll learn about the staging area, committing your code,
# branching, and merging, and how you can use these to make you more efficient
# and effective.
#
# Sjaak van den Berg
# @svdb
-->

# What happens when you initialize a repository? Why do you need to do it?

This creates an empty repository with a `.git/` directory. This lets Git know to start tracking changes.

# Updated Commands

    $ git diff                      # compare stage with working dir
    $ git diff <commit1> <commit2>  # compare commits
    $ git diff --cached             # compare stage with latest commit
    $ git clone                     # make a copy of a repo with history
    $ git checkout                  # temporarily revert all files
    $ git checkout <branch>         # checkout commit or branch
    $ git checkout -b <branch>      # create and checkout new branch
    $ git log                       # show the commit history
    $ git init                      # create new repo
    $ git add file.md               # add files to stage
    $ git commit                    # commit files
    $ git reset --hard              # reset HEAD to previous state
    $ git branch                    # show branches
    $ git branch <branch>           # create new branch
    $ git branch -d <branch>        # delete a branch
    $ git show <commit>             # show changes introduced by a commit

# Updated Concept Map

                   ╭──────╮               Symbols
                   │ init │               -------
                   ╰──────╯               ◁# operates on
                       #                  ◁- type-of
                       ▽                  ◁~ part-of
    ╭───────╮    ╱▔▔▔▔▔▔▔▔▔▔╲    ┌─────┐  ◁@ refers-to
    │ clone │ #▷ ▏repository▕ ~▷ │ Git │
    ╰───────╯    ╲▁▁▁▁▁▁▁▁▁▁╱    └─────┘
                       △            △
                       ~            ~
         ╭─────╮    ╭────────╮    ╱▔▔▔▔▔╲    ╭────────╮    ╱▔▔▔▔▔▔▔▔▔▔▔╲
         │ log │ #▷ │ commit │ #▷ ▏stage▕ ◁# │ status │ #▷ ▏working dir▕
         ╰─────╯    ╰────────╯    ╲▁▁▁▁▁╱    ╰────────╯    ╲▁▁▁▁▁▁▁▁▁▁▁╱
            #     ◁     △   △        △
            ▽   @       #   #        #
     ╭────────╮    ╭──────╮ #     ╭─────╮
     │ branch │ ◁# │ diff │ #     │ add │
     ╰────────╯    ╰──────╯ #     ╰─────╯
                        ╭───────╮
                        │ merge │
                        ╰───────╯

# How is the staging area different from the working directory and the repository? What value do you think it offers?

A staging area allows you to see which files are going to be committed. At this point, you can still unstage files that should not be committed. It's a failsafe mechanism that prevent errors.

# How can you use the staging area to make sure you have one commit per logical change?

Make sure that the staging area only contains files that have to do with the change you're committing.

# Branches

Branches are labels for commits. Master is the main branch.

                            ┌ _experimental_
                            O
                           ╱
           O -- O -- O -- O -- O
    fixbug ┘    │    │     ╲   └ _master_
    new-feature ┘    │      O
         update-docs ┘      │
                  _italian_ ┘

Checking out a branch and making a commit:

                            ┌ _experimental_
                            O
                           ╱   ┌ fix
           O -- O -- O -- O -- O -- O
    fixbug ┘    │    │     ╲        └ _*master_
    new-feature ┘    │      O
         update-docs ┘      │
                  _italian_ ┘

The current latest commit of a branch is also referred to as the tip of that branch.

# What are some situations when branches would be helpful in keeping your history organized? How would branches help?

If you like to test an alternative version of the program and keep it separate from the master branch. You might be working on a new feature, or an version that you would like to keep separated. You can track that work separately on that branch, and if needed, merge it at a later point in time.

# Commit History Diagram
                             3884eab ┐
                        3e42136 ┐    │
                   4035769 ┐    │    │
              25ede83 ┐    │    │    │
         df03538 ┐    │    │    │    │ O _easy-mode_
    b0678b1 ┐    │    │    │    │    │╱
     ... -- O -- O -- O -- O -- O -- O _master_
             ╲
              O -- O -- O -- O _coins_
      656b02e ┘    │    │    │
           a3c0ae4 ┘    │    │
                0c6daf1 ┘    │
                     354dfdd ┘

# Reachability

       f2 ┐ 3f ┐
          O -- O _a_
     e3 ┐╱
        O -- O -- O -- O _b_
          2c ┘ 7d ┘╲4d ┘
                    O
                 f3 ┘

    $ git log a # 3f, f2, e3
    $ git log b # 4d, 7d, 2c, e3

# How do the diagrams help you visualize the branch structure?

The diagrams make it easy where HEAD is, relative to other branches and commits.

# Merging Files

Jake and Rachel are editing a file.

    START   Jake    Rachel    FINAL?
    ---------------------------------
    ?       B       A         A ?
            D       B         B yes
            E       C         C ?
                    D         D yes
                              E ?
    ---------------------------------
    A       B       A         A no
    B       D       B         B yes
    D       E       C         C yes
                    D         D yes
                              E yes
    ---------------------------------
    A       A       A         A yes
    B (5°)  B' (7°) B'' (2°)  B ?
    D       D       D         B' ?
                              B'' ?
                              D yes

Coin branch can be deleted after merging.

    $ git checkout master
    $ git merge master coins -m "Merge branch 'coins'"

                             3884eab ┐
                        3e42136 ┐    │
                   4035769 ┐    │    │
              25ede83 ┐    │    │    │
         df03538 ┐    │    │    │    │ O _easy-mode_
    b0678b1 ┐    │    │    │    │    │╱   ┌ 62d8bb
     ... -- O -- O -- O -- O -- O -- O -- O -- O _*master_
             ╲                           ╱     └ ed1198
              O -- O -- O -- O ----------
      656b02e ┘    │    │    │
           a3c0ae4 ┘    │    │
                0c6daf1 ┘    │
                     354dfdd ┘

By merging the two branches, the commit history are merged into the same branched and its commits chronologically sequenced. The `git show` command shows you which changes are introduced by a commit.

# Making the Coin Yellow

    $ git checkout -b change-coin-color
    $ atom game.js # make changes to game.js
    $ git add game.js
    $ git commit -m "Give coin solid yellow color"
    $ git checkout master
    $ git merge master change-coin-color
    $ git branch -d change-coin-color

# What is the result of merging two branches together? Why do we represent it in the diagram the way we do?

It adds the changes from the non-master branch into the code of the master branch.

# Conflict Detection

Include both functions:

    foo.py              foo.py
    ---                 ---
    ---                 ---
    ---                 ---
    def new_fn:         def other_fn:
        ---                 ---
        ---                 ---
        ---                 ---

Include one function:

    foo.py              foo.py
    ---                 ---
    ---                 ---
    ---                 ---
    def new_fn:         def same_fn:
        ---                 ---
        ---                 ---
        ---                 ---

# Merging the easy-mode Branch

    $ git checkout easy-mode
    $ git merge master easy-mode
    # Auto-merging game.js
    # CONFLICT (content): Merge conflict in game.js
    # Automatic merge failed; fix conflicts and then commit the result.
    $ atom game.js

Conflicts are represented like this:

```js
<<<<<<< HEAD
      // break into fragments
      for (var i = 0; i < 2; i++) {
        var roid = $.extend(true, {}, this);
        roid.vel.x = Math.random() * 6 - 3;
        roid.vel.y = Math.random() * 6 - 3;
        if (Math.random() > 0.5) {
          roid.points.reverse();
        }
        roid.vel.rot = Math.random() * 2 - 1;
        roid.move(roid.scale * 3); // give them a little push
        Game.sprites.push(roid);
      }
=======
      this.breakIntoFragments();
>>>>>>> master
```

The code between `<<<<<<< HEAD` and `=======` in HEAD. The code between `=======` and `>>>>>>> master` is in master.

# What are the pros and cons of Git’s automatic merging vs. always doing merges manually?

Git's automatic merging may lead to unintended behavior in the program as a result of changes where the changing of connections between blocks of code break the program. Merging manually takes more effort but makes sure you know how different commits stack up.
