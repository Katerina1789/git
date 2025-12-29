# Git Project Walkthrough

**Student Name:** Katerina Kasdanastasi
**Starting Date:** December 17 2025 
**Submiting Date:** December 29 2025

---

## 1. Setting Up Git

### Install Git
I had already installed Git so I verified it by running the following command
```bash
git --version
```
and getting this output
```
git version 2.51.1
```

### Configure Git with username and email
I confirmed my credentials by running the command
```bash
git config --global --list
```
and getting this output
```
user.email=kadkat1789@gmail.com
user.name=kkasdana
credential.helper=store
```

**Challenges faced:**  
I did not remember the commands by heart.

**Solutions implemented:**  
I researched and learned them.

**Lessons learned:**  
Make in my notes a more organised, seperate command line sheet to find and memorise them easier.

---

## 2. Git Commits to Commit

### Create work directory and hello subdirectory
```bash
mkdir work
cd work
mkdir hello
```

### Create hello.sh with initial content
```bash
cd hello
code hello.sh
```
Then, I added this in the file
```
echo "Hello, World"
```

### Initialize git repository
I run this command
```bash
git init
```
and initialized empty Git repository in /var/home/... .

### Check status
By running this command,
```bash
git status
```
I can see the untracked files to commit
```
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        hello.sh

nothing added to commit but untracked files present (use "git add" to track)
```

### Stage and commit hello.sh
Now, I added the file as per the instructions
```bash
git add hello.sh
git commit -m "Initial commit: Added hello.sh"
```

### Modify hello.sh to add shebang and parameter
I modified it like this via terminal
```bash
cat > hello.sh << 'EOF'
#!/bin/bash

echo "Hello, $1"
EOF
```

### Stage and commit changes
I, then, added and commited the changes made
```bash
git add hello.sh
git commit -m "Added shebang and parameter"
```

### Add comments and make two separate commits
First, I made the changes
```bash
cat > hello.sh << 'EOF'
#!/bin/bash

# Default is "World"
name=${1:-"World"}
echo "Hello, $name"
EOF
```
Then, I staged and committed them in two separate commits
```bash
git add hello.sh
git commit -m "Added comment for default value"

git reset --soft HEAD~1

# First, add just the comment
cat > hello.sh << 'EOF'
#!/bin/bash

# Default is "World"
echo "Hello, $1"
EOF

git add hello.sh
git commit -m "Added comment for default value"

# Then add the variable logic
cat > hello.sh << 'EOF'
#!/bin/bash

# Default is "World"
name=${1:-"World"}
echo "Hello, $name"
EOF

git add hello.sh
git commit -m "Added name variable with default value"
```

**Challenges faced:**  
I got a bit confused with the steps I had to follow and their order.

**Solutions implemented:**  
I broke it down to small, simple tasks.

**Lessons learned:**  
Not to rush when deciding the order of the commands.

---

## 3. History

### Show the history of working directory
I checked my logs
```bash
git log
```
and the output was 
```bash
commit c4955186f957afbb7c2fdc3d086b4fe7af1c4295
Author: kkasdana <kadkat1789@gmail.com>
Date:   Mon Dec 29 16:24:15 2025 +0200

    Added name variable with default value

commit 60009a4476c28cc30b5d8ffaada6a3bca4e9823a
Author: kkasdana <kadkat1789@gmail.com>
Date:   Mon Dec 29 16:23:42 2025 +0200

    Added comment for default value

commit 93aff18a1bd0ccbe361665dcd7c5b035639d8f8d
Author: kkasdana <kadkat1789@gmail.com>
Date:   Mon Dec 29 16:18:06 2025 +0200

    Added shebang and parameter

commit 9d0cbc23ec22759c7e6627719371ed3990ad6b43
Author: kkasdana <kadkat1789@gmail.com>
Date:   Fri Dec 26 22:20:29 2025 +0200

    Initial commit: Added hello.sh
```

### Show One-Line History
```bash
git log --oneline
```
and the output was
```bash
c495518 (HEAD -> main) Added name variable with default value
60009a4 Added comment for default value
93aff18 Added shebang and parameter
9d0cbc2 Initial commit: Added hello.sh
```

### Display last 2 entries
```bash
git log -n 2
```
and the output was
```bash
commit c4955186f957afbb7c2fdc3d086b4fe7af1c4295 (HEAD -> main)
Author: kkasdana <kadkat1789@gmail.com>
Date:   Mon Dec 29 16:24:15 2025 +0200

    Added name variable with default value

commit 60009a4476c28cc30b5d8ffaada6a3bca4e9823a
Author: kkasdana <kadkat1789@gmail.com>
Date:   Mon Dec 29 16:23:42 2025 +0200

    Added comment for default value

```

### View commits made within last 5 minutes
```bash
git log --since="5 minutes ago"
```
and the output was blank since the commits happened earlier.

### Show logs in personalized format
```bash
git log --pretty=format:"* %h %ad | %s%d [%an]" --date=short
```
and the output was
```bash
* c495518 2025-12-29 | Added name variable with default value (HEAD -> main) [kkasdana]
* 60009a4 2025-12-29 | Added comment for default value [kkasdana]
* 93aff18 2025-12-29 | Added shebang and parameter [kkasdana]
* 9d0cbc2 2025-12-26 | Initial commit: Added hello.sh [kkasdana]
```

**Challenges faced:**  
I was taken aback by the detailed ouput when running the command "git log".

**Solutions implemented:**  
I run each command and checked out the output.

**Lessons learned:**  
New log commands which will be proven very useful.

---

## 4. Check It Out

### Restore first snapshot and print content
I searched for the first commit
```bash
git log --oneline --reverse | head -1
```
and the output was
```bash
9d0cbc2 Initial commit: Added hello.sh
```
Then, I checked out,
```bash
 git checkout 9d0cbc2
```
the output was
```bash
Note: switching to '9d0cbc2'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at 9d0cbc2 Initial commit: Added hello.sh
```
and printed the content
```bash
cat hello.sh

#!/bin/bash

echo "Hello, World"
```

### Restore second recent snapshot and print content
I checked out,
```bash
git checkout main~1
```
the output was
```bash
Previous HEAD position was 9d0cbc2 Initial commit: Added hello.sh
HEAD is now at 60009a4 Added comment for default value
```
and printed the content
```bash
cat hello.sh

#!/bin/bash

# Default is "World"
echo "Hello, $1"
```

### Return to latest version in main branch
I checked out,
```bash
git checkout main
```
the output was
```bash
Previous HEAD position was 60009a4 Added comment for default value
Switched to branch 'main'
```
and printed the content
```bash
cat hello.sh

#!/bin/bash

# Default is "World"
name=${1:-"World"}
echo "Hello, $name"
```

**Challenges faced:**  
~

**Solutions implemented:**  
~

**Lessons learned:**  
More about changing branches quickly.

---

## 5. TAG Me

### Tag current version as v1
```bash
git tag v1
```

### Tag previous version as v1-beta
```bash
git tag v1-beta HEAD~1
```

### Navigate between v1 and v1-beta
I checked out
```bash
git checkout v1-beta
```
and the output was
```bash
Note: switching to 'v1-beta'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at 60009a4 Added comment for default value
```
then, I checked out again
```bash
git checkout v1
```
and the output was
```bash
Previous HEAD position was 60009a4 Added comment for default value
HEAD is now at c495518 Added name variable with default value
```

### List all tags
I run this command
```bash
git tag
```
and the output was
```bash
v1
v1-beta
```

**Challenges faced:**  
~

**Solutions implemented:**  
~

**Lessons learned:**  
How to use tags.

---

## 6. Changed Your Mind?

### Revert unstaged changes
I made an unwanted change
```bash
cat > hello.sh << 'EOF'
#!/bin/bash

# This is a bad comment. We want to revert it.
name=${1:-"World"}

echo "Hello, $name"
EOF
```
and now I am reverting it
```bash
git checkout -- hello.sh
```

### Stage unwanted changes then clean staging area
I am making another unwanted comment
```bash
cat > hello.sh << 'EOF'
#!/bin/bash

# This is an unwanted but staged comment
name=${1:-"World"}

echo "Hello, $name"
EOF
```
and I staged it
```bash
git add hello.sh
```
Now, I am cleaning the staging area
```bash
git reset HEAD hello.sh
```
and the output was
```bash
Unstaged changes after reset:
M       hello.sh
```
lastly, I revert it
```bash
git checkout -- hello.sh
```

### Commit unwanted changes then revert
I made an unwanted change,
```bash
cat > hello.sh << 'EOF'
#!/bin/bash

# This is an unwanted but committed change
name=${1:-"World"}

echo "Hello, $name"
EOF
```
staged and commited it
```bash
git add hello.sh
git commit -m "Unwanted commit"
```
and reverted it,
```bash
git revert HEAD --no-edit
```
the output was
```bash
[main 5c0adf4] Revert "Unwanted commit"
 Date: Mon Dec 29 17:43:56 2025 +0200
 1 file changed, 1 insertion(+), 2 deletions(-)
```

### Tag latest commit as oops and reset to v1
I tagged lastest commit
```bash
git tag oops
```
and reset to v1
```bash
git reset --hard v1
```

### Display logs with deleted commits
```bash
git reflog
```
and the output was
```bash
c495518 (HEAD -> main, tag: v1) HEAD@{0}: reset: moving to v1
5c0adf4 (tag: oops) HEAD@{1}: revert: Revert "Unwanted commit"
bb6fe92 HEAD@{2}: commit: Unwanted commit
c495518 (HEAD -> main, tag: v1) HEAD@{3}: checkout: moving from c4955186f957afbb7c2fdc3d086b4fe7af1c4295 to main
c495518 (HEAD -> main, tag: v1) HEAD@{4}: checkout: moving from 60009a4476c28cc30b5d8ffaada6a3bca4e9823a to v1
60009a4 (tag: v1-beta) HEAD@{5}: checkout: moving from main to v1-beta
c495518 (HEAD -> main, tag: v1) HEAD@{6}: checkout: moving from 60009a4476c28cc30b5d8ffaada6a3bca4e9823a to main
60009a4 (tag: v1-beta) HEAD@{7}: checkout: moving from 9d0cbc23ec22759c7e6627719371ed3990ad6b43 to main~1
9d0cbc2 HEAD@{8}: checkout: moving from main to 9d0cbc2
c495518 (HEAD -> main, tag: v1) HEAD@{9}: commit: Added name variable with default value
60009a4 (tag: v1-beta) HEAD@{10}: commit: Added comment for default value
93aff18 HEAD@{11}: reset: moving to HEAD~1
c6430eb HEAD@{12}: commit: Added comment for default value
93aff18 HEAD@{13}: commit: Added shebang and parameter
9d0cbc2 HEAD@{14}: commit (initial): Initial commit: Added hello.sh
```

### Clean unreferenced commits
```bash
git reflog expire --expire=now --all
git gc --prune=now --aggressive
```
and the output was
```bash
Enumerating objects: 16, done.
Counting objects: 100% (16/16), done.
Delta compression using up to 8 threads
Compressing objects: 100% (9/9), done.
Writing objects: 100% (16/16), done.
Total 16 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
```

### Add author information and commit
Added author name,
```bash
cat > hello.sh << 'EOF'
#!/bin/bash

# Default is World
# Author: kkasdana
name=${1:-"World"}

echo "Hello, $name"
EOF
```
and added, committed change
```bash
git add hello.sh
git commit -m "Added author comment"
```

### Amend commit to add author email
Added author email,
```bash
cat > hello.sh << 'EOF'
#!/bin/bash

# Default is World
# Author: kkasdana (kadkat1789@gmail.com)
name=${1:-"World"}

echo "Hello, $name"
EOF
```
and amended commit
```bash
git add hello.sh
git commit --amend --no-edit
```

**Challenges faced:**  
There were so many things to do.

**Solutions implemented:**  
Followed the tasks step by step.

**Lessons learned:**  
To take it slow and steady.

---

## 7. Move It

### Move hello.sh to lib/ directory
First, I created the directory
```bash
mkdir lib
```
Then, I moved the file
```bash
git mv hello.sh lib/hello.sh
```
and commited the change
```bash
git commit -m "Moved hello.sh to lib directory"
```

### Create and commit Makefile
I created the Makefile
```bash
cat > Makefile << 'EOF'
TARGET="lib/hello.sh"

run:
	bash ${TARGET}
EOF
```
and committed it
```bash
git add Makefile
git commit -m "Added Makefile"
```

**Challenges faced:**  
~

**Solutions implemented:**  
~

**Lessons learned:**  
Revised how to move and create directories and files via terminal.

---

## 8. Blobs, Trees and Commits

### Navigate to .git/ directory and list contents
I navigated to the .git/
```bash
ls -la .git/
```

**Explanation of subdirectories:**
- `objects/`: Stores all content (blobs, trees, commits)
- `config`: Repository-specific configuration
- `refs/`: References to commits (branches, tags)
- `HEAD`: Points to current branch

### Find latest object hash
```bash
git rev-parse HEAD
```
and the output was
```bash
89949e5f6e2686e8c1e52cfead24f2db266afeb2
```

### Print type and content of object'
I printed the type
```bash
git cat-file -t HEAD
```
and the output was
```bash
commit
```
Then, I printed the content
```bash
git cat-file -p HEAD
```
and the output was
```bash
tree 2eebe1ecf92e041116c336f93028c89099b8acd4
parent 49b88ee6cc748ba5ea54059984be5e1bf2adcdc7
author kkasdana <kadkat1789@gmail.com> 1767024089 +0200
committer kkasdana <kadkat1789@gmail.com> 1767024089 +0200

Added Makefile
```

### Dump directory tree referenced by commit
I got the tree hash
```bash
git cat-file -p HEAD
```
and dumped the tree
```bash
git cat-file -p 2eebe1ecf92e041116c336f93028c89099b8acd4
```
and the output was
```bash
100644 blob 407082da4bc68dba41102de9599b0a7c9def931b    Makefile
040000 tree d061ba9e778fc7a8c75fd1120894b362ecac6e1c    lib
```

### Dump contents of lib/ directory and hello.sh
I got the hash,
```bash
git cat-file -p 2eebe1ecf92e041116c336f93028c89099b8acd4 | grep lib
```
dumped the contents
```bash
git cat-file -p d061ba9e778fc7a8c75fd1120894b362ecac6e1c
```
and dumped hello.sh content
```bash
git cat-file -p 6aabe69341b5be7d4713613335fcaf853f7e7c0d 
```
and the output was
```bash
#!/bin/bash

# Default is World
# Author: kkasdana (kadkat1789@gmail.com)
name=${1:-"World"}

echo "Hello, $name"
```

**Challenges faced:**  
~

**Solutions implemented:**  
~

**Lessons learned:**  
How to use the "git cat-file" commands.

---

## 9. Branching

### Create and switch to greet branch
```bash
git checkout -b greet
```
and the output was
```bash
Switched to a new branch 'greet'
```

### Create greeter.sh in lib directory
I created the file
```bash
cat > lib/greeter.sh << 'EOF'
#!/bin/bash

Greeter() {
    who="$1"
    echo "Hello, $who"
}
EOF
```
and committed it
```bash
git add lib/greeter.sh
git commit -m "Added greeter.sh with Greeter function"
```

### Update lib/hello.sh
```bash
cat > lib/hello.sh << 'EOF'
#!/bin/bash

source lib/greeter.sh

name="$1"
if [ -z "$name" ]; then
    name="World"
fi

Greeter "$name"
EOF
```
and committed it
```bash
git add lib/hello.sh
git commit -m "Updated hello.sh to use Greeter function"
```

### Update Makefile with comment
```bash
cat > Makefile << 'EOF'
# Ensure it runs the updated lib/hello.sh file
TARGET="lib/hello.sh"

run:
	bash ${TARGET}
EOF
```
and committed it
```bash
git add Makefile
git commit -m "Updated Makefile with comment"
```

### Switch to main and compare branches
I checked out,
```bash
git checkout main
```
compared the files
```bash
git diff main greet -- Makefile
git diff main greet -- lib/hello.sh
git diff main greet -- lib/greeter.sh
```
and the output was
```bash
diff --git a/Makefile b/Makefile
index 407082d..12d4ffb 100644
--- a/Makefile
+++ b/Makefile
@@ -1,3 +1,4 @@
+# Ensure it runs the updated lib/hello.sh file
 TARGET="lib/hello.sh"
 
 run:
diff --git a/lib/hello.sh b/lib/hello.sh
index 6aabe69..38c758b 100644
--- a/lib/hello.sh
+++ b/lib/hello.sh
@@ -1,7 +1,10 @@
 #!/bin/bash
 
-# Default is World
-# Author: kkasdana (kadkat1789@gmail.com)
-name=${1:-"World"}
+source lib/greeter.sh
 
-echo "Hello, $name"
+name="$1"
+if [ -z "$name" ]; then
+    name="World"
+fi
+
+Greeter "$name"
diff --git a/lib/greeter.sh b/lib/greeter.sh
new file mode 100644
index 0000000..2d14ca5
--- /dev/null
+++ b/lib/greeter.sh
@@ -0,0 +1,6 @@
+#!/bin/bash
+
+Greeter() {
+    who="$1"
+    echo "Hello, $who"
+}
```

### Create and commit README.md
Created it
```bash
cat > README.md << 'EOF'
This is the Hello World example from the git project.
EOF
```
and committed it
```bash
git add README.md
git commit -m "Added README.md"
```

### Draw commit tree diagram
```bash
git log --all --graph --decorate --oneline
```
and the output was
```bash
* ea543de (HEAD -> main) Added README.md
| * 6554d37 (greet) Updated Makefile with comment
| * 6c34afb Updated hello.sh to use Greeter function
| * 3e249e2 Added greeter.sh with Greeter function
|/  
* 89949e5 Added Makefile
* 49b88ee Moved hello.sh to lib directory
* 172c89b Added author comment
| * 5c0adf4 (tag: oops) Revert "Unwanted commit"
| * bb6fe92 Unwanted commit
|/  
* c495518 (tag: v1) Added name variable with default value
* 60009a4 (tag: v1-beta) Added comment for default value
* 93aff18 Added shebang and parameter
* 9d0cbc2 Initial commit: Added hello.sh
```

**Challenges faced:**  
~

**Solutions implemented:**  
~

**Lessons learned:**  
To compare files and navigate through the branches.

---

## 10. Conflicts, Merging and Rebasing

### Merge main into greet branch
I checked out
```bash
git checkout greet
```
and merged them,
```bash
git merge main -m "Merged main into greet"
```
the output was
```bash
Merge made by the 'ort' strategy.
 README.md | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 README.md
 ```

### Switch to main branch and make changes to hello.sh file
I checked out,
```bash
git checkout main
```
modified the file
```bash
cat > lib/hello.sh << 'EOF'
#!/bin/bash

echo "What's your name"
read my_name

echo "Hello, $my_name"
EOF
```
and committed it
```bash
git add lib/hello.sh
git commit -m "Modified hello.sh to ask for name"
```

### Merging main into greet branch (Conflict)
```bash
git checkout greet
git merge main
```

### Resolve the conflict (manually or using merge tools)
```bash
git checkout greet
git merge main
```
the output was
```bash
Switched to branch 'greet'
Auto-merging lib/hello.sh
CONFLICT (content): Merge conflict in lib/hello.sh
Automatic merge failed; fix conflicts and then commit the result.
```

### After resolving, stage the changes and commit
```bash
git checkout --theirs lib/hello.sh
```
and commit it
```bash
git add lib/hello.sh
git commit -m "Resolved conflict: accepted main branch changes"
```

### Rebasing greet branch
I went back
```bash
git checkout greet
git reset --hard HEAD~2
```
rebased
```bash
git rebase main
```

### Merging greet into main
I checked out
```bash
git checkout main
```
and merged
```bash
git merge greet
```
the output was
```bash
Updating 918009b..eb19915
Fast-forward
 Makefile       |  1 +
 lib/greeter.sh |  6 ++++++
 lib/hello.sh   | 10 +++++++---
 3 files changed, 14 insertions(+), 3 deletions(-)
 create mode 100644 lib/greeter.sh
 ```

**Understanding Fast-Forwarding:**  
Moving branch pointer forward when no divergent changes exist.

**Difference between Merging:**  
Creates a merge commit, preserves history of both branches.

**Difference between Rebasing:**  
Replays commits on top of another branch, creates linear history

**Challenges faced:**  
The complexity of the conflicts confused me a bit.

**Solutions implemented:**  
Studied the commands more.

**Lessons learned:**  
Study what each command does seperately.

---

## 11. Local and Remote Repositories

### Clone hello repository as cloned_hello
```bash
cd ../
git clone hello cloned_hello
```
and the output was
```bash
Cloning into 'cloned_hello'...
done.
```

### Show logs for cloned repository
```bash
cd cloned_hello
git log --oneline
```
and the output was
```bash
eb19915 (HEAD -> main, origin/main, origin/greet, origin/HEAD) Updated Makefile with comment
9f8cce8 Updated hello.sh to use Greeter function
11830a2 Added greeter.sh with Greeter function
918009b Modified hello.sh to ask for name
ea543de Added README.md
89949e5 Added Makefile
49b88ee Moved hello.sh to lib directory
:...skipping...
eb19915 (HEAD -> main, origin/main, origin/greet, origin/HEAD) Updated Makefile with comment
9f8cce8 Updated hello.sh to use Greeter function
11830a2 Added greeter.sh with Greeter function
918009b Modified hello.sh to ask for name
ea543de Added README.md
89949e5 Added Makefile
49b88ee Moved hello.sh to lib directory
172c89b Added author comment
:...skipping...
eb19915 (HEAD -> main, origin/main, origin/greet, origin/HEAD) Updated Makefile with comment
9f8cce8 Updated hello.sh to use Greeter function
11830a2 Added greeter.sh with Greeter function
918009b Modified hello.sh to ask for name
ea543de Added README.md
89949e5 Added Makefile
49b88ee Moved hello.sh to lib directory
172c89b Added author comment
c495518 (tag: v1) Added name variable with default value
60009a4 (tag: v1-beta) Added comment for default value
:...skipping...
eb19915 (HEAD -> main, origin/main, origin/greet, origin/HEAD) Updated Makefile with comment
9f8cce8 Updated hello.sh to use Greeter function
11830a2 Added greeter.sh with Greeter function
918009b Modified hello.sh to ask for name
ea543de Added README.md
89949e5 Added Makefile
49b88ee Moved hello.sh to lib directory
172c89b Added author comment
c495518 (tag: v1) Added name variable with default value
60009a4 (tag: v1-beta) Added comment for default value
93aff18 Added shebang and parameter
:...skipping...
eb19915 (HEAD -> main, origin/main, origin/greet, origin/HEAD) Updated Makefile with comment
9f8cce8 Updated hello.sh to use Greeter function
11830a2 Added greeter.sh with Greeter function
918009b Modified hello.sh to ask for name
ea543de Added README.md
89949e5 Added Makefile
49b88ee Moved hello.sh to lib directory
172c89b Added author comment
c495518 (tag: v1) Added name variable with default value
60009a4 (tag: v1-beta) Added comment for default value
93aff18 Added shebang and parameter
9d0cbc2 Initial commit: Added hello.sh
:...skipping...
eb19915 (HEAD -> main, origin/main, origin/greet, origin/HEAD) Updated Makefile with comment
9f8cce8 Updated hello.sh to use Greeter function
11830a2 Added greeter.sh with Greeter function
918009b Modified hello.sh to ask for name
ea543de Added README.md
89949e5 Added Makefile
49b88ee Moved hello.sh to lib directory
172c89b Added author comment
c495518 (tag: v1) Added name variable with default value
60009a4 (tag: v1-beta) Added comment for default value
93aff18 Added shebang and parameter
9d0cbc2 Initial commit: Added hello.sh
~
(END)...skipping...
eb19915 (HEAD -> main, origin/main, origin/greet, origin/HEAD) Updated Makefile with comment
9f8cce8 Updated hello.sh to use Greeter function
11830a2 Added greeter.sh with Greeter function
918009b Modified hello.sh to ask for name
ea543de Added README.md
89949e5 Added Makefile
49b88ee Moved hello.sh to lib directory
172c89b Added author comment
c495518 (tag: v1) Added name variable with default value
60009a4 (tag: v1-beta) Added comment for default value
93aff18 Added shebang and parameter
9d0cbc2 Initial commit: Added hello.sh
~
~
(END)...skipping...
eb19915 (HEAD -> main, origin/main, origin/greet, origin/HEAD) Updated Makefile with comment
9f8cce8 Updated hello.sh to use Greeter function
11830a2 Added greeter.sh with Greeter function
918009b Modified hello.sh to ask for name
ea543de Added README.md
89949e5 Added Makefile
49b88ee Moved hello.sh to lib directory
172c89b Added author comment
c495518 (tag: v1) Added name variable with default value
60009a4 (tag: v1-beta) Added comment for default value
93aff18 Added shebang and parameter
9d0cbc2 Initial commit: Added hello.sh
~
~
~
(END)...skipping...
eb19915 (HEAD -> main, origin/main, origin/greet, origin/HEAD) Updated Makefile with comment
9f8cce8 Updated hello.sh to use Greeter function
11830a2 Added greeter.sh with Greeter function
918009b Modified hello.sh to ask for name
ea543de Added README.md
89949e5 Added Makefile
49b88ee Moved hello.sh to lib directory
172c89b Added author comment
c495518 (tag: v1) Added name variable with default value
60009a4 (tag: v1-beta) Added comment for default value
93aff18 Added shebang and parameter
9d0cbc2 Initial commit: Added hello.sh
~
~
~
~
(END)...skipping...
eb19915 (HEAD -> main, origin/main, origin/greet, origin/HEAD) Updated Makefile with comment
9f8cce8 Updated hello.sh to use Greeter function
11830a2 Added greeter.sh with Greeter function
918009b Modified hello.sh to ask for name
ea543de Added README.md
89949e5 Added Makefile
49b88ee Moved hello.sh to lib directory
172c89b Added author comment
c495518 (tag: v1) Added name variable with default value
60009a4 (tag: v1-beta) Added comment for default value
93aff18 Added shebang and parameter
9d0cbc2 Initial commit: Added hello.sh
~
~
~
~
~
(END)...skipping...
eb19915 (HEAD -> main, origin/main, origin/greet, origin/HEAD) Updated Makefile with comment
9f8cce8 Updated hello.sh to use Greeter function
11830a2 Added greeter.sh with Greeter function
918009b Modified hello.sh to ask for name
ea543de Added README.md
89949e5 Added Makefile
49b88ee Moved hello.sh to lib directory
172c89b Added author comment
c495518 (tag: v1) Added name variable with default value
60009a4 (tag: v1-beta) Added comment for default value
93aff18 Added shebang and parameter
9d0cbc2 Initial commit: Added hello.sh
~
~
~
~
~
~
(END)...skipping...
eb19915 (HEAD -> main, origin/main, origin/greet, origin/HEAD) Updated Makefile with comment
9f8cce8 Updated hello.sh to use Greeter function
11830a2 Added greeter.sh with Greeter function
918009b Modified hello.sh to ask for name
ea543de Added README.md
89949e5 Added Makefile
49b88ee Moved hello.sh to lib directory
172c89b Added author comment
c495518 (tag: v1) Added name variable with default value
60009a4 (tag: v1-beta) Added comment for default value
93aff18 Added shebang and parameter
9d0cbc2 Initial commit: Added hello.sh
~
~
~
~
~
~
~
(END)...skipping...
eb19915 (HEAD -> main, origin/main, origin/greet, origin/HEAD) Updated Makefile with comment
9f8cce8 Updated hello.sh to use Greeter function
11830a2 Added greeter.sh with Greeter function
918009b Modified hello.sh to ask for name
ea543de Added README.md
89949e5 Added Makefile
49b88ee Moved hello.sh to lib directory
172c89b Added author comment
c495518 (tag: v1) Added name variable with default value
60009a4 (tag: v1-beta) Added comment for default value
93aff18 Added shebang and parameter
9d0cbc2 Initial commit: Added hello.sh
~
~
~
~
~
~
~
~
(END)...skipping...
eb19915 (HEAD -> main, origin/main, origin/greet, origin/HEAD) Updated Makefile with comment
9f8cce8 Updated hello.sh to use Greeter function
11830a2 Added greeter.sh with Greeter function
918009b Modified hello.sh to ask for name
ea543de Added README.md
89949e5 Added Makefile
49b88ee Moved hello.sh to lib directory
172c89b Added author comment
c495518 (tag: v1) Added name variable with default value
60009a4 (tag: v1-beta) Added comment for default value
93aff18 Added shebang and parameter
9d0cbc2 Initial commit: Added hello.sh
~
~
~
~
~
~
~
~
~
(END)...skipping...
eb19915 (HEAD -> main, origin/main, origin/greet, origin/HEAD) Updated Makefile with comment
9f8cce8 Updated hello.sh to use Greeter function
11830a2 Added greeter.sh with Greeter function
918009b Modified hello.sh to ask for name
ea543de Added README.md
89949e5 Added Makefile
49b88ee Moved hello.sh to lib directory
172c89b Added author comment
c495518 (tag: v1) Added name variable with default value
60009a4 (tag: v1-beta) Added comment for default value
93aff18 Added shebang and parameter
9d0cbc2 Initial commit: Added hello.sh
```

### Display name of remote repository
```bash
git remote
git remote -v
git remote show origin
```
and the output was
```bash
origin
origin  /var/home/bbyg/VS Code/git/work/hello (fetch)
origin  /var/home/bbyg/VS Code/git/work/hello (push)
* remote origin
  Fetch URL: /var/home/bbyg/VS Code/git/work/hello
  Push  URL: /var/home/bbyg/VS Code/git/work/hello
  HEAD branch: main
  Remote branches:
    greet tracked
    main  tracked
  Local branch configured for 'git pull':
    main merges with remote main
  Local ref configured for 'git push':
    main pushes to main (up to date)
```

### List all remote and local branches
```bash
git branch -a
```
and the output was
```bash
* main
  remotes/origin/HEAD -> origin/main
  remotes/origin/greet
  remotes/origin/main
```

### Make changes to original repository and commit
Entered the location,
```bash
cd ../hello
```
modified the file
```bash
cat > README.md << 'EOF'
This is the Hello World example from the git project.
(changed in the original)
EOF
```
and committed it
```bash
git add README.md
git commit -m "Updated README in original repository"
```

### Fetch changes from remote in cloned_hello
```bash
cd ../cloned_hello
git fetch
git log --all
```

### Merge changes from remote main branch
```bash
git merge origin/main
```
the output was
```bash
Updating eb19915..a4caf58
Fast-forward
 README.md | 1 +
 1 file changed, 1 insertion(+)
```

### Add local branch greet tracking remote origin/greet
```bash
git checkout -b greet origin/greet
```
and the output was
```bash
branch 'greet' set up to track 'origin/greet'.
Switched to a new branch 'greet'
```

### Add remote and push main and greet branches
```bash
cd ../hello
git remote add origin https://platform.zone01.gr/git/kkasdana/git.git
git push -u origin main
git push origin greet
git push --tags
```

**Answer to audit question:**  
"What is the single git command equivalent to what you did before to bring changes from remote to local main branch?"  
**Answer:** git pull

**Challenges faced:**  
I got confused a few times.

**Solutions implemented:**  
Took it step by step.

**Lessons learned:**  
To be more patient.

---

## 12. Bare Repositories

**What is a bare repository and why is it needed?**  
A repository without a working directory, used as a central shared repository and it is needed for collaboration, acts as a central hub where developers push/pull changes.

### Create bare repository hello.git
```bash
cd /var/home/bbyg/VS\ Code/git/work
git clone --bare hello hello.git
```
and the output was
```bash
Cloning into bare repository 'hello.git'...
done.
```

### Add bare repository as remote to original hello
```bash
cd hello
git remote add shared ../hello.git
```

### Change README.md and push to shared repository
Modified README.md file
```bash
cat > README.md << 'EOF'
This is the Hello World example from the git project.
(Changed in the original and pushed to shared)
EOF
```
and push the changes
```bash
git add README.md
git commit -m "Updated README for shared repository"
git push shared main
git push shared greet
```

### Pull changes in cloned_hello from shared repository
```bash
cd ../cloned_hello
git remote add shared ../hello.git
git pull shared main
```

**Challenges faced:**  
Understanding merge vs rebase and managing conflicts.

**Solutions implemented:**  
Followed the tasks step by step.

**Lessons learned:**  
How Git tracks changes and manages collaboration.

---

## Summary

**Overall challenges:**  
Learning Git commands and branching strategies.

**Key takeaways:**  
Git is essential for version control and teamwork.

**Time spent:**  
8 hours

**Additional notes:**  
This project taught me Git fundamentals for real-world use.
