# TASK 1

## Command outputs for object insepction

1. Commit Inspection
```bash
> git cat-file -p ac414a9
tree 21740bcc2f3b90702f1c7236a78a108fe619b182
parent 6a7370d345414435648918ab614bab6d74117475
author sasaSilver <al.mikhailov@innopolis.university> 1770741344 +0300
committer sasaSilver <al.mikhailov@innopolis.university> 1770741344 +0300
gpgsig -----BEGIN SSH SIGNATURE-----
 U1NIU0lHAAAAAQAAADMAAAALc3NoLWVkMjU1MTkAAAAgVTPzmoKbth5TJzSwVKjgadsxlM
 Q1ET0CE7Z6PX/SJ28AAAADZ2l0AAAAAAAAAAZzaGE1MTIAAABTAAAAC3NzaC1lZDI1NTE5
 AAAAQECypzc+Q2e0SIz90y+MUWf7pBeixRl6IQEJOJKgmDMU31X0bIf9DP4BSOenSJAD2b
 lPOf/13+ayYZxR+s81YwM=
 -----END SSH SIGNATURE-----

Add test file
```

2. Tree Inspection
```bash
> git cat-file -p 21740bcc2f3b90702f1c7236a78a108fe619b182
040000 tree b1240785fc0c3a6352a44eef786e4dc5fdba3ef9    .github
100644 blob 6e60bebec0724892a7c82c52183d0a7b467cb6bb    README.md
040000 tree a1061247fd38ef2a568735939f86af7b1000f83c    app
040000 tree eb79e5a468ab89b024bd4f3ed867c6a3954fe1f0    labs
040000 tree d3fb3722b7a867a83efde73c57c49b5ab3e62c63    lectures
100644 blob 2eec599a1130d2ff231309bb776d1989b97c6ab2    test.txt
```

3. Blob Inspection
```bash
> git cat-file -p 2eec599a1130d2ff231309bb776d1989b97c6ab2
Test content
```

Blob represents contents of a file, tree represents repository structure, and commit represents a snapshot of the repository

Git stores repository data as immutable objects-blobs for file contents, trees for directories, and commits for snapshots, each identified by a hash. These objects form a directed acyclic graph where commits link to parent commits, creating a complete version history. References such as branches and tags are mutable pointers that track specific commits.

The examples of these objects are provided above after using `git cat-file` command.

# TASK 2

The commands I ran:

1. `git reset --soft HEAD~1`. It moved the HEAD pointer back one commit but kept the changes of the last commit in the working tree. It can be used to make changes to the last local (not pushed yet) commit.

2. `git reset --hard HEAD~1`. Moved the HEAD pointer back again but discarded the changes last commit introduced from the working tree. It can be used to completely redo a breaking commit.

3. `git reflog`. Showed the movement of the HEAD pointer. It can be used to view (and debug) the history of the repository (what commits were made, which were reverted, etc.)

4. `git reset --hard f4252f2`. The commit hash is of the third commit. It moved the HEAD to my last commit and discarded any other changes.

I think a typical recovery process (in case of a breaking commit, for example) will include:

1. Using reflog to find the hash of the commit before the breaking one.

2. Running `git restore --hard (or --soft) <safe_commit_hash>` to return the repo to a safe state.

3. Pushing with `git push` to remote.

# TASK 3

1. Graph snippet and commit messages list

```bash
> git log --oneline --graph --all
* c025a3f (side-branch) Side branch commit
* ac414a9 (HEAD -> feature/lab2) Add test file
| * 26e82ac (origin/feature/lab1, feature/lab1) feat: lab1 task2 PR templates
| * 0c7be06 feat: lab1 task1 ssh setup
|/  
* 6a7370d (origin/main, origin/HEAD, main) feat: add pr template
* d6b6a03 Update lab2
* 87810a0 feat: remove old Exam Exemption Policy
* 1e1c32b feat: update structure
* 6c27ee7 feat: publish lecs 9 & 10
* 1826c36 feat: update lab7
* 3049f08 feat: publish lec8
* da8f635 feat: introduce all labs and revised structure
* 04b174e feat: publish lab and lec #5
* 67f12f1 feat: publish labs 4&5, revise others
* 82d1989 feat: publish lab3 and lec3
* 3f80c83 feat: publish lec2
* 499f2ba feat: publish lab2
* af0da89 feat: update lab1
* 74a8c27 Publish lab1
* f0485c0 Publish lec1
...
```

3. I think git graph provides value by showing the commit/merge history of the repository (what branches were merged, what commits were made on them, what parent branches they originated from) like a DAG.

# TASK 4

1. The tag name is `v1.0.0` as in the example, made with `git tag v1.0.0`.

2. Hash of the tagged commit is `ac414a9ede083525303c1421f41cb4d0420ae1a7`.

3. I think tags are needed to distinguish commits that complete a feature/release. Many commits can be made before, but when a final commit that introduces a working goal is made, it can be tagged to distinguish that point. I think tags are most useful in GitHub flow, where there is only long-lived branch. For Git flow, I think they are not that useful as the main branch is usually never kept in an itermediate state during a making of a feature/release.

# TASK 5

1.
```bash
> git switch -c cmd-compare
Switched to a new branch 'cmd-compare'
```

```bash
> git checkout -b cmd-compare-2
Switched to a new branch 'cmd-compare-2'
```

```bash
> echo "scratch" >> demo.txt
> git add demo.txt
> git restore --staged demo.txt # unstaged demo.txt
> git add demo.txt
> git commit -m "init scratch"
[cmd-compare-2 c2e934d] init scratch
 1 file changed, 1 insertion(+)
 create mode 100644 demo.txt
> echo "scratch2" > demo.txt
> git restore --source=HEAD~1 demo.txt # removed the file, as it was added only on this commit
> git restore demo.txt # brought the file back
> git restore --source=HEAD~1 demo.txt # ran for the next task
```

2.
```bash
git status
On branch cmd-compare-2
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        deleted:    demo.txt
```

```bash
> git branch
  cmd-compare
* cmd-compare-2
  feature/lab1
  feature/lab2
  main
  side-branch
```

3. As said in the lab, switch is used to __switch__ between branches or create new ones, same with checkout but it does more than needed. Restore __restores__ file state from commit hash.

# TASK 6

I starred the mentioned repos, followed the TAs and the professor.

I think starring on github matters for their ability to deilver discovery, an "upvote", or a "like" in a sence like another social media but for GitHub and developers.

Following, just like in any other SNS, is a way to keep up with collegues/friends as developers. In team projects especially. For example, if a project is multi-repo, then you can better follow who does what in each one. And it delivers networking in a sense as well.
