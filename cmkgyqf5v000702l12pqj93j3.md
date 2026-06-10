---
title: "Git Explained: How the .git Folder Powers Your Project's History"
seoTitle: "Understanding the .git Folder in Projects"
seoDescription: "Explore how the .git folder and objects within power your project's version history with Git's elegant system"
datePublished: 2026-01-16T14:17:35.299Z
cuid: cmkgyqf5v000702l12pqj93j3
slug: git-explained-how-the-git-folder-powers-your-projects-history
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1768572972608/293e04ff-dcbe-454a-9bc8-9531cd965723.png
tags: github, git, git-internals-how-git-works-git-vs-github-git-folder-explained

---

Have you ever wondered what actually happens when you run `git add` or `git commit`? Most developers use Git daily, memorizing commands without understanding the elegant system working behind the scenes. Let's build a mental model of how Git really works by exploring its internal structure.

## The .git Folder: Git's Brain

When you run `git init` in a directory, Git creates a `.git` folder. This hidden folder is the entire repository—it contains everything Git needs to track your project's history. If you delete `.git`, you lose all version control (but not your current files).

Let's explore what's inside:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1768576502543/60b1649e-4235-45d0-9876-4b60cceeef77.png align="center")

The two most important components are:

* **objects/** - Git's database where all content lives
    
* **refs/** - Pointers to specific commits (your branches)
    

## Git Objects: The Building Blocks

Git stores everything as objects in the `objects/` directory. There are four main types you need to understand:

### 1\. Blob (Binary Large Object)

A blob stores the **content of a file**. That's it—just the content, no filename, no metadata. When you save a file, Git compresses it and stores it as a blob.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1768577045792/3060bd06-053d-4975-8aff-408c403e9499.png align="center")

### 2\. Tree

A tree is like a directory listing. It stores:

* Filenames
    
* File permissions (mode)
    
* Pointers to blobs (for files) or other trees (for subdirectories)
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1768579812870/424164c6-8405-49e9-b4de-c7a6ea738483.png align="center")

### 3\. Commit

A commit object stores:

* Pointer to a tree (snapshot of your project)
    
* Pointer to parent commit(s)
    
* Author and committer information
    
* Timestamp
    
* Commit message
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1768579947263/c2e04a36-5e01-4c21-a872-a7061c31efb9.png align="center")

### 4\. Tag (Annotated)

A tag object stores:

* Pointer to a commit (or other object)
    
* Tagger information
    
* Tag message
    

While lightweight tags are just references, annotated tags are full objects stored in the database.

## How Git Objects Relate to Each Other

Here's the beautiful part—these objects form a graph that represents your entire project history:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1768579996552/54529799-ebe3-4748-a802-00546eb752c9.png align="center")

Each commit points to a complete snapshot of your project through its tree. The tree points to blobs (files) and other trees (subdirectories).

## Git Hashes: Ensuring Integrity

Every Git object gets a unique identifier—a 40-character SHA-1 hash. This hash is computed from the object's content.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1768580000542/57d979fe-2da0-4cee-b3cc-2f4d9926a1c4.png align="center")

**Why this matters:**

* If content changes even slightly, the hash changes completely
    
* Impossible to corrupt data without Git detecting it
    
* Two identical files get the same hash (Git stores them once)
    
* Commits reference trees and blobs by hash, creating a tamper-proof history
    

## What Happens During `git add`?

When you run `git add filename`, here's what Git does internally:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1768580047928/87f1b150-86ef-431a-b405-f0c689a7ee1d.png align="center")

**Step by step:**

1. **Git computes the hash** of `app.js` content
    
2. **Git compresses the content** and stores it as a blob in `.git/objects/`
    
3. **Git updates the index** (staging area) to point to this blob
    

The index is a binary file (`.git/index`) that tracks which blobs should be included in the next commit.

## What Happens During `git commit`?

When you run `git commit -m "message"`, Git creates two new objects:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1768580054607/f79cc1c1-867f-4af2-9774-f36975b340dd.png align="center")

**Step by step:**

1. **Git creates a tree object** representing the current staging area
    
    * Lists all files and their blob hashes
        
    * Lists all subdirectories and their tree hashes
        
2. **Git creates a commit object** pointing to:
    
    * The new tree (project snapshot)
        
    * The parent commit (previous commit)
        
    * Your commit message and metadata
        
3. **Git updates the branch pointer** (in `.git/refs/heads/main`) to point to the new commit
    

## The Complete Flow: From Edit to Commit

Let's trace what happens when you edit a file and commit:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1768580066252/5d79b1cc-b057-4856-9b7e-918833a25a97.png align="center")

## Branches Are Just Pointers

Here's a mind-blowing realization: branches in Git are just text files containing a commit hash!

```bash
$ cat .git/refs/heads/main
c5a9d3f8e2b1a4c7d9f3e8b2a5c1d4f7e9b3c6a8

$ cat .git/HEAD
ref: refs/heads/main
```

When you create a branch, Git just creates a new file in `.git/refs/heads/`. When you switch branches, Git updates `.git/HEAD` to point to a different branch file. That's it!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1768580073814/e790b334-e4c6-4547-b44c-5210d38f264d.png align="center")

## Building Your Mental Model

Now you can understand Git commands differently:

* `git add` = "Store this file content as a blob and update the index"
    
* `git commit` = "Create a tree from the index, create a commit pointing to it, and move the branch pointer"
    
* `git branch` = "Create a new pointer to the current commit"
    
* `git checkout` / `git switch` = "Move HEAD to a different branch and update working directory to match that commit's tree"
    
* `git merge` = "Create a new commit with two parents"
    

## Why This Matters

Understanding Git internals helps you:

1. **Debug issues confidently** - You know where Git stores everything
    
2. **Understand error messages** - Terms like "detached HEAD" make sense
    
3. **Recover from mistakes** - You know commits are never truly deleted (until garbage collection)
    
4. **Use advanced features** - Rebasing, cherry-picking, and bisecting become logical
    
5. **Trust Git** - You understand its integrity guarantees
    

## Experiment Yourself

Try these commands to explore your `.git` folder:

```bash
# See all objects Git has created
find .git/objects -type f

# See what type an object is
git cat-file -t <hash>

# See the content of an object
git cat-file -p <hash>

# See what's in the staging area
git ls-files --stage

# See the current commit your branch points to
cat .git/refs/heads/main
```

## Conclusion

Git isn't magic—it's an elegant content-addressable filesystem with a simple object model. Every file is a blob, every directory is a tree, every snapshot is a commit, and branches are just pointers. The `.git` folder contains this entire beautiful graph structure.

Next time you run `git commit`, visualize Git creating those tree and commit objects, storing them by their hash, and updating a branch pointer. You're not just saving changes—you're building an immutable, tamper-proof graph of your project's history.

Now go forth and commit with confidence! 🚀

---

*Found this helpful? Let me know in the comments what clicked for you, or what you'd like to explore deeper!*