# How did viewing a diff between two versions of a file help you see the bug that was introduced?

By using `diff`, you can immediately see the additions, edits and removals that happened between two files. I use `colordiff` to colorize the output, so that differences also visually stand out.

# How could having easy access to the entire history of a file make you a more efficient programmer in the long term?

It makes it easier to spot at which point in the revision history bugs were introduced to a program. It also enables you to revert back to an earlier version of a program, should the need arise.

# Concept Map
                                      Symbols △▽▷◁
╭───────╮    ╱▔▔▔▔▔▔▔▔▔▔╲   ┌─────┐   ◁= operates on
│ Clone │ =▷ ▏repository▕ -▷│ Git │   ◁- type-of
╰───────╯    ╲▁▁▁▁▁▁▁▁▁▁╱   └─────┘   ◁* part-of
                   △
                   |
   ╭─────╮    ╭────────╮    ╭──────╮
   │ Log │ =▷ │ Commit │ ◁= │ Diff │
   ╰─────╯    ╰────────╯    ╰──────╯

# Feature Comparison Chart

                 Any       Use        Manual
                 Editor    Offline    Save
Manual Saving    ✓         ✓          ✓
Dropbox          ✓         ×          ×
Google Docs      ×         ×          ×
Wikipedia        ×         ×          ✓
Git              ✓         ✓          ✓
SVN              ✓         ×          ✓

# Commit Size

One commit per logical change.

# What do you think are the pros and cons of manually choosing when to create a commit, like you do in Git, vs having versions automatically saved, like Google docs does?

Manually committing forces you to get into the habit of making commented commits when logical changes to a program are made. Automatically having versions saved lacks logical structure to the points of revision, making it difficult to backtrack. It does take away the need to commit manually.

# Why do you think some version control systems, like Git, allow saving multiple files in one commit, while others, like Google Docs, treat each file separately?

In some cases, files are related to each other and need to be tracked together.

# How can you use the commands git log and git diff to view the history of files?

`git log` shows you a history of commits with their commit authors, ids and messages. `git diff` allows you to compare the edits in two different commits against each other.

# How might using version control make you more confident to make changes that could break something?

You can always revert to an earlier state and undo the breaking changes.

# Now that you have your workspace set up, what do you want to try using Git for?

A test repo.

# Commands So Far

$ git diff      # compare commits
$ git clone     # make a copy of a repository, including commit history
$ git checkout  # temporarily reset all files to a previous state
$ git log       # show the commit history
$ git init      # create new repo
