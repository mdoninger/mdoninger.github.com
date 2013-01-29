---
layout: page
title: "How to use git filter-branch to remove files from a repository"
description: ""
group: git
---
{% include JB/setup %}

<div class="alert alert-error">
<h4>Attention!</h4>
All operations in this tutorial should be executed with caution! Always backup your repository before starting, or use a new clone
of your repository! If you do anything wrong, don't blame me!
</div>

If you have a Git repository, which resulted from a migration from CVS or Subversion, or if someone accidentally committed
some binary files, which bloats your repository, you may want to remove those files (or whole folder) from the whole Git history
in that repository.

The command git filter-branch walks through the history of the repository, and on every commit you can execute additional scripts
or programs to manipulate this commit.
