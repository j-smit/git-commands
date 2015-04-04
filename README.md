# git-commands
This is a summary from [atlassion.com](https://de.atlassian.com/git/)

## Most important Steps/Commands

1. **Project Start**
	- **Create Repo**: `git init` optional with `<directory>` (in specific directory)
	- **Clone Repo**: `git clone <repo>` optional with `<directory>` (into directory)
2. **Inspecting Repo**
	- **Display State**: `git status`
	- **List history** `git log`
	
3. **Workflow**
 	1. **Collaborating**
		- **Branches:** `git branch` (list branch) with `<newBranch>` (create new)
		- **Navigate between branches**: `git checkout` with `<branchname>`(use already created) or `-b <new-branch>` (first create and then use)
		- **Integrate Branches** `git merge` with `<branchname>`


	2. **Save Changes**
		- **Stage Changes**: `git add` `<file>` or `<directory>` or `.` 
		- **Commit staged snapshot**: `git commit` optional with `-m "your message"` or `-a` (only tracked files)
4. **Resolving Conflicts**	


##Getting Started

###Setting up a repository (one-time operation)

#### `git init`
The `git init` command creates a new Git repository.  It can be used to convert an existing, unversioned project to a Git repository or initialize a new empty repository.

- `git init` : Transform the current directory into a Git repository.
- `git init <directory>` : Create an empty Git repository in the specified directory. 
- `git init --bare <directory>` : Initialize an empty Git repository, but omit the working directory. 

#### `git clone`
The `git clone` command copies an existing Git repository. This is sort of like `svn checkout`, except the “working copy” is a full-fledged Git repository—it has its own history, manages its own files, and is a completely isolated environment from the original repository.

- `git clone <repo>` : Clone the repository located at <repo> onto the local machine.
- `git clone <repo> <directory>` : Clone the repository located at <repo> into the folder called <directory> on the local machine.


#### `git config`
The `git config` command lets you configure your Git installation (or an individual repository) from the command line. This command can define everything from user info to preferences to the behavior of a repository. 

The `--global` flag is used to set configuration options in all git repositories. 

- `git config user.name <name>`: Define the author name to be used for all commits in the current repository. 
- `git config --global user.name <name>`: Define the author name to be used for all commits by the current user.
- `git config --global user.email <email>`: Define the author email to be used for all commits by the current user.
- `git config --global alias.<alias-name> <git-command>`: Create a shortcut for a Git command.
- `git config --system core.editor <editor>`: Define the text editor used by commands like git commit for all users on the current machine. The <editor> argument should be the command that launches the desired editor (e.g., vi).
- `git config --global --edit`: Open the global configuration file in a text editor for manual editing.

#####Git stores configuration options in three separate files
1. `<repo>/.git/config`: Repository-specific settings.
2. `~/.gitconfig`: User-specific settings. This is where options set with the `--global` flag are stored.
3. `$(prefix)/etc/gitconfig`: System-wide settings.

When options in these files conflict, local settings override user settings, which override system-wide. If you open any of these files, you’ll see something like the following:

	[user] 
	name = John Smith
	email = john@example.com
	[alias]
	st = status
	co = checkout
	br = branch
	up = rebase
	ci = commit
	[core]
	kueditor = vim
	
### Saving changes (`git add` and `git commit`)
These are the two commands that every Git user needs to understand, regardless of their team’s collaboration model. They are the means to record versions of a project into the repository’s history.

Developing a project revolves around the basic edit/stage/commit pattern. 

1. First, you edit your files in the working directory. 
2. When you’re ready to save a copy of the current state of the project, **you stage changes** with `git add`. 
3. After you’re happy with the staged snapshot, **you commit** it to the project history with `git commit`.

**staying area**: Instead of committing all of the changes you've made since the last commit, the stage lets you group related changes into highly focused snapshots before actually committing it to the project history.

It helps to think of it as a buffer between the working directory and the project history.



#### `git add`
The `git add` command adds a change in the working directory to the staging area. It tells Git that you want to include updates to a particular file in the next commit. However, `git add` doesn't really affect the repository in any significant way—changes are not actually recorded until you run `git commit`.

- `git add <file>`: Stage all changes in <file> for the next commit.
- `git add <directory>`: Stage all changes in `<directory>` for the next commit.
- `git add -p`: Begin an interactive staging session that **lets you choose portions of a file to add** to the next commit.
	This will present you with a chunk of changes and prompt you for a command.
		- Use `y` to stage the chunk, 
		- `n` to ignore the chunk,
		- `s` to split it into smaller chunks,
		- `e` to manually edit the chunk,
		- and `q` to exit.

#### `git commit`
The `git commit` command commits the staged snapshot to the project history. Snapshots are committed to the local repository, and this requires absolutely no interaction with other Git repositories.

- `git commit`: Commit the staged snapshot. This will launch a text editor prompting you for a commit message.
- `git commit -m "your message"`: Commit the staged snapshot, but instead of launching a text editor, use `<message>` as the commit message.
- `git commit -a`: Commit a snapshot of all changes in the working directory. This only includes modifications to tracked files (those that have been added with `git add` at some point in their history).

 

#####Vim Editor
- To **save** your work and **exit** press: `Esc` and `:` `w` `q`  (w for write and q for quit).
- Both **save** and **exit** press: `Esc` and `:` `x`
- Both **save** and **exit** press: `Esc` and `:` `ZZ`
- **Exit** without saving you can hit `:` `q!`

[To Cheatsheet Vim](http://www.fprintf.net/vimCheatSheet.html)

###Inspecting a repository

#### `git status`
The `git status` command displays the state of the working directory and the staging area. It lets you see which changes have been staged, which haven’t, and which files aren’t being tracked by Git.

**It‘s good practice to check the state of your repository** before committing changes so that you don’t accidentally commit something you don't mean to

- `git status`: List which files are staged, unstaged, and untracked.


#### `git log`
The `git log` command displays committed snapshots. It lets you list the project history, filter it, and search for specific changes. 

- `git log`: Display the entire commit history using the default formatting. If the output takes up more than one screen, you can use `Space` to **scroll** and `q` to **exit**.
- `git log -n <limit>`: Limit the number of commits by <limit>. For example, ***git log -n 3*** will display only 3 commits.
- `git log --oneline`: Condense each commit to a single line. This is useful for getting a high-level overview of the project history.
- `git log --stat`: Along with the ordinary `git log` information, include which files were altered and the relative number of lines that were added or deleted from each of them.
- ``

	
## Collaborating


###Using Branches
Git branches aren't like SVN branches. Whereas SVN branches are only used to capture the occasional large-scale development effort, Git branches are an integral part of your everyday workflow.

####`git branch`
A branch represents an independent line of development. Branches serve as an abstraction for the edit/stage/commit process. You can think of them as:

- a way to request a brand new working directory, 
- staging area, 
- and project history.

The `git branch` command lets you create, list, rename, and delete branches. 

- `git branch`: List all of the branches in your repository.
- `git branch <newBranch>`: Create a new branch called <branch>. This does not check out the new branch.
- `git branch -d <branch>`: Delete the specified branch. This is a “safe” operation in that Git prevents you from deleting the branch if it has unmerged changes.
- `git branch -D <branch>`: Force delete the specified branch, even if it has unmerged changes. This is the command to use if you want to permanently throw away all of the commits associated with a particular line of development.
- `git branch -m <branch>`: Rename the current branch to <branch>.

#### `git checkout`
The `git checkout` command lets you navigate between the branches created by git branch. Checking out a branch updates the files in the working directory to match the version stored in that branch, and it tells Git to record all new commits on that branch. Think of it as a way to select which line of development you’re working on.

- `git checkout <existing-branch>`: Check out the specified branch, which should have already been created with `git branch`. This makes <existing-branch> the current branch, and updates the working directory to match.
- `git checkout -b <new-branch>`: Create and check out <new-branch>. The `-b` option is a convenience flag that tells Git to run `git branch <new-branch>` before running `git checkout <new-branch>`. 
- `git checkout -b <new-branch> <existing-branch>`: Same as the above invocation, but base the new branch off of <existing-branch> instead of the current branch.

#### `git merge`
Merging is Git's way of putting a forked history back together again. The `git merge` command lets you take the independent lines of development created by `git branch` and integrate them into a single branch.

- `git merge <branch>`: Merge the specified branch into the current branch. Git will determine the merge algorithm automatically.
- `git merge --no-ff <branch>`: Merge the specified branch into the current branch, but always generate a merge commit (even if it was a fast-forward merge). This is useful for documenting all merges that occur in your repository.




## Resolving Merge Conflicts
If the two branches you‘re trying to merge both changed the same part of the same file, Git won’t be able to figure out which version to use. When such a situation occurs, it stops right before the merge commit so that you can resolve the conflicts manually.

##Advanced Tips

###Reset, Checkout, and Revert
The git reset, git checkout, and git revert command are some of the most useful tools in your Git toolbox. They all let you undo some kind of change in your repository, and the first two commands can be used to manipulate either commits or individual files.

#### `git reset`







####Problem solving
- Cannot rebase because of uncommitted changes
	1. `git stash`: stores the different files away from everything else, returning your working directory to the last commit.
	2. `git pull --rebase`
	3. `git stash`: This will return those files to the working directory and allow you to work as before.

	
	