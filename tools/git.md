# GIT

git-init to create a new repository.

git-log to see what happened.

git-checkout and git-branch to switch branches.

git-add to manage the index file.

git-diff and git-status to see what you are in the middle of doing.

git-commit to advance the current branch.

git-reset and git-checkout (with pathname parameters) to undo changes.

git-merge to merge between local branches.

git-rebase to maintain topic branches.

git-tag to mark a known point.

git-clone from the upstream to prime your local repository.

git-pull and git-fetch from "origin" to keep up-to-date with the upstream.

git-push to shared repository, if you adopt CVS style shared repository workflow.

git-format-patch to prepare e-mail submission, if you adopt Linux kernel-style public forum workflow.

git-send-email to send your e-mail submission without corruption by your MUA.

git-request-pull to create a summary of changes for your upstream to pull.

git-am to apply patches e-mailed in from your contributors.

git-pull to merge from your trusted lieutenants.

git-format-patch to prepare and send suggested alternative to contributors.

git-revert to undo botched commits.

git-push to publish the bleeding edge.

git-daemon to allow anonymous download from repository.

git-shell can be used as a restricted login shell for shared central repository users.

git-http-backend provides a server side implementation of Git-over-HTTP ("Smart http") allowing both fetch and push services.

gitweb provides a web front-end to Git repositories, which can be set-up using the git-instaweb script.

git-reflog The reflog is Git's internal record of every explicit change we've made

reflog show <branch-name> to see the records of branch

Git's command interface is generally considered somewhat confusing and inconsistent. Luckily, beneath the command interface is a wonderfully consistent and straightforward object model. By gaining an understanding of the object model, we can easily wrap our heads around even the most complex Git operation by thinking in terms of these objects.

In this video, we'll lay the foundation of the Git object model, describing exactly how Git stores and references our code.

To help illustrate the points of our discussion, we'll create a file with the classic hello world as the contents.

$ echo 'hello world' > readme.md
Git RepositoryJump to Topic In Video
To begin the discussion on the Git object model, we'll need a Git repository. The "repository" is the hidden directory .git/ which contains all of the objects Git uses to track our revisions, such as branches, remotes, etc. Starting from an empty directory, we'll run:

$ git init
and Git kindly creates the repository for us.

Here are the contents of the .git/ directory immediately after running git init:

$ tree .git
.git
├── HEAD
├── config
├── description
├── hooks/
│   ├── applypatch-msg.sample
|   └── # ... (other hooks)
├── info/
│   └── exclude
├── objects/
│   ├── info/
│   └── pack/
└── refs/
    ├── heads/
    └── tags/
The .git directory contains a handful of files and subdirectories (ending with a /), even if nothing has been tracked yet. In this discussion, we'll be focusing on the following paths:

Name	Function
HEAD	A "pointer" to the currently checked out object (more on this later).
objects/	Where Git stores its representation of all files, directories, and commits.
refs/	Where Git stores all branches, tags, remotes, etc.
config, description, hooks/, and info/ contain metadata, and we can ignore them during this discussion.

Adding Our First ObjectJump to Topic In Video
First, we'll be focusing on the objects/ directory. It's best to think about this directory as a mini file-based database where Git will store its representation of our files, directories, and commits.

If we take a peek at the objects/ directory, we'll see that it remains empty. Git does not run on its own in the background.

If we run git status, we see that Git is aware there is a new file, but has not started tracking it. Thus, the file is not in the .git/objects directory yet.

$ git add readme.md
Now we'll take another look, and see that we have our first Git object!

$ tree -I "info|pack" .git/objects
.git/objects
└── 3b
    └── 18e512dba79e4c8300dd08aeb37f8e728b8dad
(The -I bit means ignore the provided pattern. Those files aren't relevant to our discussion.)

Here we can see a new directory and file. Every object in Git has a unique 40-character hex string as its name, and Git uses this name to store the file (this technique is called content-addressable storage). Git takes the first 2 characters of the object's name and uses them as the directory, with the remaining 38 as the file name. We'll ignore this subtlety going forward, as it is a performance optimization, but it is good to know for later on.

BlobsJump to Topic In Video
This first object we've added to our Git repository is a "blob." Git uses blobs to track files, but you should note that a blob stores only the contents of our file, not the name. We can see this by asking Git to show us the contents of the first object it has stored using the cat-file command and the object's name (note that we only need to provide the first eight or so characters from the name, not the whole name):

$ git cat-file -p 3b18e512
hello world
Again, we see here that Git is only storing the contents of the file, namely hello world. Other information like the mode, permissions, and file name is stored elsewhere.

Because Git only stores the contents of the file rather than the name or any metadata, it can tell when you are giving a different name to the same version of a file and therefore process it quickly. If we have two files with identical content but different names, the content has only been stored once!

Hashing OverviewJump to Topic In Video
When storing our file, Git uses a "blob" which only concerns itself with the contents of the file, ignoring our filename (for now). However, it does need a name, and we've seen that Git uses a seemingly random 40-character hex string as the name.

It turns out this string is in fact not random at all, but is produced by taking the content that Git stores and running it through a "hash function," the SHA-1 hash function in this case. The hash function takes a string of any size as an input, and returns a 40-character hex string as the output.

SHA-1 has a number of useful properties, but the most important to Git are:

Determinism - The same input will always result in the same output.
Defined range - All outputs are 40 char hex.
Uniformity - Outputs are evenly distributed over the possible space, and a small change in input yields a huge change in output.
The use of these hash values as the names for our objects makes operations like deep comparison of files and directories easy, as we're only comparing the hash values. Going forward, we'll refer to these names as a "hash."

Object Storage SubtletiesJump to Topic In Video
We're close to fully understanding how Git stores our file, but if we try to replicate the hash function on the content "hello world," it doesn't match with the 3b18e512... hash.

$ echo 'hello world' | shasum
22596363b3de40b06f981fb85d82312e8c0ed511  -
This is because Git prepends a bit of metadata before the object contents, specifically the object type, length, and a separator character, and then passes the combined string through the hash function, available as shasum:

$ echo -e 'blob 12\0hello world' | shasum
3b18e512dba79e4c8300dd08aeb37f8e728b8dad  -
Now we have a complete understanding of how Git names and stores our blob objects. Git uses a similar metadata structure for the other object types, but from here on we'll only discuss the primary content of the Git objects, ignoring the metadata.

This metadata has the benefit of allowing us (and Git!) to know the type of an object in isolation. Let's check the object's type with the -t, for "type", flag passed to cat-file:

$ git cat-file -t 3b18e512
blob
TreesJump to Topic In Video
It wouldn't be very useful if we could only track the contents of files, and not even the file names or the structure. This is where "tree" objects come in. A "tree" in Git is an object (a file, really) which contains a list of pointers to blobs or other trees. Each line in the tree object's file contains a pointer (the object's hash) to one such object (tree or blob), while also providing the mode, object type, and a name for the file or directory.

$ git add readme.md
$ git commit -m 'Add readme'
$ tree -I "info|pack" .git/objects
.git/objects
├── 3b
│   └── 18e512dba79e4c8300dd08aeb37f8e728b8dad
├── 73
│   └── 94b8cc9ca916312a79ce8078c34b49b1617718
└── ef
    └── 34a153025fffb8a498fff540f7c93963937291
In committing our readme.md file, we create two new objects. One is the object for the commit itself, but the other, ef34a15..., is the new "tree" object that represents our current directory. (Remember that the full hash for an object is its directory name prepended to the file name, ef and 34a15... in this case). We can view it with:

$ git cat-file -t ef34a15
tree

$ git cat-file -p ef34a15
100644 blob 3b18e512dba79e4c8300dd08aeb37f8e728b8dad    readme.md
Our new tree object consists of a single line, listing the mode/permissions, the type, the hash, and the file name of our readme.md file.

Again, we'll note that tree objects themselves do not have names, much like blobs. Parent trees associate names for subtrees, and the root tree, referred to as the "working tree" of a repository, in fact has no name.

This has two fun characteristics:

The repo doesn't care what you call it. You can rename your local directory that contains your repository to anything you'd like. Git is blissfully unaware of the name of the directory that contains the .git repo directory.
We can rename subtrees as much as we want, and only parent objects need to update. The subtree object itself and everything below remain untouched.
SubtreesJump to Topic In Video
Trees require at least one file, and optionally have subtrees. An empty directory would yield an empty tree, and this is why we can't track empty directories in Git and have to use tricks like adding a hidden .gitkeep file into the directory. (Technically, there's no strict reason for this limitation, it's just that no one has fixed it... ¯\_(ツ)_/¯)

We'll create a subtree with:

$ mkdir app
$ touch app/script.rb
$ git add --all
$ git status
## master
A  app/script.rb
$ git commit -m 'Another file in app Dir'
Looking in the objects/ directory, there are now multiple new objects.

Of most interest to us is the new tree object for our working directory, our current root tree. Since there are so many objects now, we can't just guess which is which, but we can ask Git directly to show us a specific tree using the ls-tree command.

$ git ls-tree master
040000 tree 67b21f78a4548b2ba3eab318bb3628d039e851e6    app
100644 blob 3b18e512dba79e4c8300dd08aeb37f8e728b8dad    readme.md
We passed master as the "tree" to view since master, a branch, points at a commit, which points at a tree. By passing master as the argument, we're identifying the tree master indirectly points at.

We have a new tree object and it contains a new line, the first line, identifying a subtree for our app subdirectory. We can view the tree by grabbing its hash and running:

$ git ls-tree 67b21f78a4548b2ba3eab318bb3628d039e851e6
100644 blob e69de29bb2d1d6434b8b29ae775ad8c2e48c5391    script.rb
And here we see a single line for the script.rb file in the app directory. This rounds out our understanding of trees. To review:

Trees list out the contents of a directory (blobs and subtrees).
For each object, the mode, permissions, type, hash, and name is listed.
Tree objects must contain at least one blob or tree.
Trees can be nested to any depth.
Trees, like blobs, don't store names. The names are stored in parent trees.
Trees are named and stored in the objects/ directory by hashing their contents (the list of objects described above).
CommitJump to Topic In Video
A commit is the final piece in our object puzzle, and it connects all of the other objects together, acting as the hub of our object graph. Just like with our other objects, we can use cat-file -p to get a pretty printed view of how Git stores commit objects.

$ git log --oneline --decorate
* f95b2fe (HEAD -> master) Another file in app dir
* ef34a15 Add readme

$ git cat-file -p f95b2fe
tree 0cae7dc167b255c0123c7c396fc48ce40fc35cfa
parent ef34a153025fffb8a498fff540f7c93963937291
author Chris Toomey <chris@ctoomey.com> 1441311544 -0400
committer Chris Toomey <chris@ctoomey.com> 1441311544 -0400

Another file in app dir
A commit is a file, just like our blob and tree objects, with a specific structure. That structure includes:

The hash of the working tree - This is always a single tree, never more, never less. The tree can point to any number of subtrees, but for every version of our code there is one root working tree.
The hash of the parent commit(s) - Git tracks the history by simply pointing at the previous commit. In the case of a merge, there can be multiple parent commits, or, in the case of the root commit, no parents.
The author info and date.
The commiter info and date.
The full commit message.
This file is then passed through the SHA-1 hash function and saved alongside our other objects in the .git/objects directory.

It's worth noting that the commit object only contains a single reference to a working directory; Git doesn't store diffs. When diffing between two commits, it compares the working trees of the commits, computing the diff on demand.

Walking the Git Object GraphJump to Topic In Video
Commits are the core of the Git object graph, and we'll explore this by walking this graph just a bit:

# using the "parent" commit hash from above
$ git cat-file -p ef34a153025fffb8a498fff540f7c93963937291
tree 7394b8cc9ca916312a79ce8078c34b49b1617718
author Chris Toomey <chris@ctoomey.com> 1441311368 -0400
committer Chris Toomey <chris@ctoomey.com> 1441311368 -0400

Add readme
Here we've walked the graph and viewed the parent commit, which we see is the root commit (as it has no parent), and now we go a step further to view the working tree of this parent commit:

$ git cat-file -p 7394b8cc9ca916312a79ce8078c34b49b1617718
100644 blob 3b18e512dba79e4c8300dd08aeb37f8e728b8dad    readme.md
Here we see the initial directory with the single script.rb file, and finally:

$ git cat-file -p 3b18e512dba79e4c8300dd08aeb37f8e728b8dad
hello world

Welcome back to our tour of the Git object model. In this video, we'll go beyond the base objects and look at more of the structure with tags, branches, and remotes, as well as reviewing how the various Git commands act on this collection of objects.

Note - If you haven't watched the First Part of this review of the Git object model, we highly recommend you go back and do that now, as this video largely builds on that foundation.

Git Object ReviewJump to Topic In Video
Before adding more to our growing picture of the Git object model, let's quickly review the base objects we covered in the first video:

Blobs - Our base objects, storing the contents of a single version of a file.
Trees - Trees store directory listings, pointing at blobs and other trees to define a full directory structure.
Commits - Commits lock in a version of our code, pointing at a single tree, the "working tree", as well as holding the commit message and author info. Commits also point at parent commits to capture the history of our code.
RefsJump to Topic In Video
Returning to our peek into the .git directory, we can first review the layout:

$ tree .git -L 1
.git
├── COMMIT_EDITMSG
├── HEAD
├── config
├── description
├── hooks/
├── index
├── info/
├── logs/
├── objects/
└── refs/
In the previous video, we focused primarily on the objects directory, which acted as a database of the blob, tree, and commit objects we created as we worked with our repo.

In this video, we'll instead focus on the refs directory. Peeking inside, we'll see:

$ tree .git/refs
.git/refs
├── heads/
|   └── master
└── tags/
HeadsJump to Topic In Video

The first directory we'll encounter within the refs directory is heads. These are our local branches. The directory is called heads, as our local branches are the collection of things that HEAD can point at.HEAD is the ultimate ref, defining what we currently have checked out.

Currently, our heads directory only contains a single file, master. We call this master file a "file", rather than some more complex Git object, because that it what it is. We can test this by cating it out:

$ cat .git/refs/heads/master
f95b2fe3b64c6351e7eec4011921b4469098b9ba
Here we can see that the file contains a string which looks very much like a Git object hash. We can then turn around and ask Git about the object:

$ git cat-file -t f95b2fe3b64c6351e7eec4011921b4469098b9ba
commit

$ git cat-file -p f95b2fe3b64c6351e7eec4011921b4469098b9ba
tree 0cae7dc167b255c0123c7c396fc48ce40fc35cfa
parent ef34a153025fffb8a498fff540f7c93963937291
author Chris Toomey <chris@ctoomey.com> 1441311544 -0400
committer Chris Toomey <chris@ctoomey.com> 1441311544 -0400

Another file in app dir
Now we have a full picture of what exactly our master branch is: a file, stored in .git/refs/heads. Its contents are the hash of a single commit. We know that commits contain a pointer to the working tree, as well as parent commits, and now we can add branches to the list of pointers in our view of the Git world.

Branches are just pointers; nothing more!

TagsJump to Topic In Video

Now that we have an understanding of branches, we can shift our focus to tags. We'll create a tag by running git tag v0.1, and then we can take another look at our .git/refs directory to see what we have:

$ tree .git/refs
.git/refs
├── heads/
|   └── master
└── tags/
    └── v0.1
Now we have a new file, v0.1, stored in the tags directory. Similar to the master head file, we can cat out the tag file directly to see what it contains:

$ cat .git/refs/tags/v0.1
f95b2fe3b64c6351e7eec4011921b4469098b9ba
Just like our master file, the v0.1 file contains nothing more than the hash of a commit. It is possible for tags, unlike branches, to grow a bit more complex by adding things like annotations, PGP signatures, and other metadata. In this case, they will be stored in the .git/objects directory, and the tag file will simply contain the hash of that tag object (which will contain the hash of the commit that was tagged).This just adds one additional step, so we can still think of tags as simple pointers to commits.

Difference Between Tags and BranchesJump to Topic In Video

While branches and tags are very similar in that they both simply contain a reference to a commit, they differ in that branches can change what they point at, but tags cannot.

Tags exist to lock down and name ("tag", if you will) a specific version of the code. Branches exist to track the changes in our codebase over time, and will therefore update whenever we commit or merge.

Remote BranchesJump to Topic In Video

For the small local sample repo we've been working with so far there are no remotes, but we can hop over to the local checkout of the Upcase repo to see an example that contains remotes:

$ tree .git/refs
.git/refs
├── heads/
|   ├── deck-last-attempt
|   ├── master
|   ├── ... (truncated)
|   └── welcome-trail
├── remotes/
│   ├── origin
│   │   ├── HEAD
│   │   ├── cjt-north-star-metric
│   │   ├── master
│   │   ├── mg-button-colors
│   │   └── ... (truncated)
│   ├── production
│   │   └── master
│   └── staging
│       ├── dashboard-staging
│       ├── ... (truncated)
│       └── master
└── tags/
    └── v0.1
With the more real-world example of the Upcase Git repo, we can see that there is now a third subdirectory alongside heads and tags in the .git/refs directory.

Within this remotes directory, there is a directory for each of our remotes, namely origin, staging, and production. This adds a bit more structure, but otherwise these objects are the same as our branches. We can confirm this by investigating the contents of one of these remote branch files:

$ cat .git/refs/origin/cjt-north-star-endpoint
3891a7bc21e5e0c69e71e8153bb8b4a67b80bff5

$ git cat-file -t 3891a7bc21e5e0c69e71e8153bb8b4a67b80bff5
commit

$ git cat-file -p 3891a7bc21e5e0c69e71e8153bb8b4a67b80bff5
tree 32022b6465ebf9f9e37b7e1caccb3c9e620dd465
parent 7262141ae317f56b567ed2f95505e6ca9bbe1605
author Chris Toomey <chris@ctoomey.com> 1433384047 -0400
committer Chris Toomey <chris@ctoomey.com> 1435239388 -0400

WIP analytics JSON endpoint
Again, we see more of the same. Remote branches are simply pointers to a commit. It's pointers all the way down, friends!

HEAD ObjectJump to Topic In Video
HEAD is the final object we need to be aware of to understand Git. HEAD, unlike the other objects we've discussed, is a singleton, meaning that there is only ever one HEAD.

HEAD identifies the currently checked out object. Typically, this is a branch (with that branch pointing to a commit), but it is possible to check out a commit directly, in which case HEAD would be pointing at that commit.

HEAD is a file just like our branch objects. It lives at the root of the .git/ directory and its contents are similarly simple:

$ cat .git/HEAD
ref: refs/heads/master
This is the normal mode for Git, where HEAD points to a branch, in this case the master branch. If we were to check out a commit directly, then HEAD would simply point at that commit:

$ git co 833c1ea

$ cat .git/HEAD
833c1ea55d76adcf48b5f7e933271fcc3e36f123
So once again we find ourselves with a pointer. HEAD points to a branch, that branch points to a commit, and that commit points to a working tree and parent commit. Pointers. All. The. Way. Down.

Final Object Model DiagramJump to Topic In Video
And, with the addition of HEAD, we have a complete picture of the Git object model.

Objects - blobs, trees, and commits.
Refs - branches, tags, and remote branches.
HEAD - The single pointer to rule them all.
Git Object Model

Git Operations and ObjectsJump to Topic In Video
Now that we understand the objects that are used throughout Git, we're going to zoom out a bit and focus primarily on commits and refs. Nearly all operations in Git involve commits, although typically these commits are referenced through refs like branches and remotes.

CheckoutJump to Topic In Video

Checking out a new branch is just the act of creating a ref file, specifically a "head", and populating it with the relevant commit hash.

$ git checkout -b new-branch
First Git will follow from the HEAD to the current branch to determine what commit hash that branch points at. With that info, Git creates a new file in .git/refs/headswith our new branch name as the file name, and the commit hash as the contents. Lastly, it updates HEAD to point at this new ref.

Verbose CheckoutJump to Topic In Video

Similarly, we can use the verbose form of checkout, where we explicitly specify the base branch. For instance:

$ git checkout -b other-branch master
is largely the same as the last check out, but instead of starting from HEAD, we start from the specified branch to determine the commit to point at, and use that to populate our new ref file.

Checking Out a FileJump to Topic In Video

There's an alternative form of checkout when we check out a file by specifying a ref. Technically, we need a tree to get to a specific version of a file, but Git's pointer system also allows for something to be "tree-ish". When something is tree-ish, it will eventually lead to a single tree by dereferencing the pointers.

A commit is tree-ish because commits point at a single tree for the working directory.

Refs are tree-ish because they point at commits, which point at a tree.

Even HEAD is tree-ish by the same logic.

So if we use the following form of the checkout command:

$ git checkout master -- app/assets/javascripts/application.js
Git will begin by looking up the commit that master points at, then the working tree of that commit, and then walk down through the intermediate trees until it reaches the blob for app/assets/javascripts/application.js, and restore that version of the file.

CommittingJump to Topic In Video

Committing takes all of the staged objects and stores them as needed. This typically involves at least one new blob, and a new tree for the current version of the working directory.

It then builds a commit object that points at our new tree, as well as the commit we are currently on.

Lastly, it updates our checked out branch to point at this newly created commit.

$ git commit -m "Add new file"
Fast-Forward MergeJump to Topic In Video

A fast-forward merge is about the simplest operation we can perform. It creates no new objects, instead simply updating the current branch to reference a different commit.

$ git merge --ff-only feature
MergeJump to Topic In Video

A traditional merge is much more interesting. We start with two diverging histories, and Git creates a new tree for us from the two existing trees.

Once it has the new tree, Git will create a new commit that points at this tree. Lastly, the branch ref will be updated to point at this new commit.

Comparing these two merge strategies, it becomes clear why we prefer the fast-forward only merges. In a fast-forward merge we are just updating a pointer, but the code is not changed. In a traditional merge, Git does its best to bring together two different versions of the code, creating a new commit and tree that we have not interacted with.

$ git merge feature
RebasingJump to Topic In Video

So with this comparison of traditional and fast-forward merges in mind, we can talk about our good friend rebase. Rebase can be performed when we have new commits on both our feature branch, and our "upstream" branch (typically master). We want to update the commits on our branch so they include the changes on master.

When we rebase, we essentially replay our work on the current version of the upstream branch. Git does this by calculating each of the diffs for the commits unique to our branch, then applies them onto the upstream branch one by one. Each application of a diff creates a new commit, reusing the associated commit message and author details.

Note that the old commits still exist, but they are now orphaned. No refs point to them any longer and so they are essentially unreachable, although we know from the discussion of the reflog in the first video that we could easily restore them by checking the reflog.

Once all the new commits have been created, our branch is updated to point at the tip commit of our rebased group.

From here, we could now fast-forward merge the master branch into ours, as we are now in line with its history. The key difference between this and a traditional merge is that all of the commits here were created by us, and we get to interact with them and test them as needed before merging them into master.

$ git rebase master
Interactive RebaseJump to Topic In Video

Interactive rebase is very similar. We begin with a set of commits, typically on a feature branch and ahead of master, and we perform our interactive rebase. When we squash them down, we create a new commit using the tree of our former tip commit, and compose a new commit message.

Once again, we can see that the old commits live on despite being orphaned, and we can therefore get back to them as needed.

$ git rebase --interactve master

- https://github.com/jkulak/git-ninja/blob/master/README.md#toc

More info:
- https://www.learnenough.com/git-tutorial
- https://wildlyinaccurate.com/a-hackers-guide-to-git/
- https://maryrosecook.com/blog/post/git-from-the-inside-out
- https://davidwalsh.name/checkout-previous-branch-git
- https://medium.com/walmartlabs/nitty-gitties-69998e14cc92
- https://vimeo.com/146478456
- https://github.com/blynn/gitmagic
- https://github.com/git-tips/tips
