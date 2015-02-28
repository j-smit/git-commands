# git-commands
This is a summary from [atlassion.com](https://de.atlassian.com/git/)
##Setting up a repository (one-time operation)

##`git init`
The `git init` command creates a new Git repository.  It can be used to convert an existing, unversioned project to a Git repository or initialize a new empty repository.

- `git init` : Transform the current directory into a Git repository.
- `git init <directory>` : Create an empty Git repository in the specified directory. 
- `git init --bare <directory>` : Initialize an empty Git repository, but omit the working directory. 

##`git clone`
The `git clone` command copies an existing Git repository. This is sort of like `svn checkout`, except the “working copy” is a full-fledged Git repository—it has its own history, manages its own files, and is a completely isolated environment from the original repository.

- `git clone <repo>` : Clone the repository located at <repo> onto the local machine.
- `git clone <repo> <directory>` : Clone the repository located at <repo> into the folder called <directory> on the local machine.


##`git config`
The `git config` command lets you configure your Git installation (or an individual repository) from the command line. This command can define everything from user info to preferences to the behavior of a repository. 

The `--global` flag is used to set configuration options in all git repositories. 

- `git config user.name <name>`: Define the author name to be used for all commits in the current repository. 
- `git config --global user.name <name>`: Define the author name to be used for all commits by the current user.
- `git config --global user.email <email>`: Define the author email to be used for all commits by the current user.
- `git config --global alias.<alias-name> <git-command>`: Create a shortcut for a Git command.
- `git config --system core.editor <editor>`: Define the text editor used by commands like git commit for all users on the current machine. The <editor> argument should be the command that launches the desired editor (e.g., vi).
- `git config --global --edit`: Open the global configuration file in a text editor for manual editing.

###Git stores configuration options in three separate files
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
	editor = vim