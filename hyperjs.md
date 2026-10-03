Absolutely. Below is a complete **start-to-finish reference guide** based on the setup we actually configured, including installation, configuration, `.bashrc`, Starship customization, zoxide, fzf, Git aliases, shortcuts, troubleshooting, and how to modify everything later.

# Windows Developer Terminal Setup

A practical developer-terminal setup for Windows using:

* Hyper
* Git Bash
* Cascadia Code PL
* Starship
* zoxide
* fzf
* Git aliases
* Node.js / npm shortcuts
* Python / uv shortcuts
* Nerd Font icons
* Customized Starship prompt

The goal is a clean, fast terminal suitable for daily development.

---

# 1. Final Setup Overview

The final architecture is:

```text
Windows
│
├── Hyper
│   └── Git Bash
│
├── Cascadia Code PL
│
├── Starship
│   ├── Directory
│   ├── Git branch
│   ├── Git status
│   ├── Node.js version
│   ├── Python version
│   ├── Docker context
│   └── Command duration
│
├── zoxide
│   └── Fast directory navigation
│
├── fzf
│   ├── Ctrl + R → history search
│   ├── Ctrl + T → file search
│   └── Alt + C → directory search
│
└── Git aliases
    └── Short commands for daily Git operations
```

---

# 2. Install Git for Windows

Install Git for Windows.

Git Bash comes with Git for Windows.

After installation, verify:

```bash
git --version
```

Check Git Bash:

```bash
bash --version
```

You should be able to open:

```text
Git Bash
```

---

# 3. Install Hyper

Install Hyper Terminal.

Hyper will be used as the main terminal application.

The important part is configuring Hyper to use Git Bash instead of the default Windows shell.

Open Hyper's configuration:

```text
Ctrl + ,
```

or open its configuration file.

The important configuration is:

```js
shell: 'C:\\Program Files\\Git\\bin\\bash.exe',
shellArgs: ['--login'],
```

This makes Hyper start Git Bash automatically.

After changing Hyper configuration, restart Hyper.

---

# 4. Verify Git Bash Inside Hyper

Open Hyper and run:

```bash
echo $SHELL
```

You should get something similar to:

```text
/usr/bin/bash
```

Also test:

```bash
pwd
```

and:

```bash
ls
```

If these work, Hyper is successfully running Git Bash.

---

# 5. Install Cascadia Code PL

Install:

```text
Cascadia Code PL
```

The `PL` version is important because it contains Powerline/Nerd-style glyphs.

Set Hyper's font to:

```js
fontFamily: '"Cascadia Code PL", Consolas, monospace',
```

A suitable font configuration is:

```js
fontSize: 14,
fontFamily: '"Cascadia Code PL", Consolas, monospace',
lineHeight: 1.15,
letterSpacing: 0,
```

---

# 6. Test Icon Support

Before configuring Starship icons, test the font.

Run:

```bash
printf '\ue61c\n'
```

Then:

```bash
printf '\ue0b0\n'
```

Then:

```bash
printf '\uf489\n'
```

Then:

```bash
printf '\uf1d8\n'
```

If you see proper symbols instead of boxes, your font is working.

For this setup, Cascadia Code PL is sufficient.

There is no need to install another Nerd Font.

---

# 7. Starship Installation

Starship is responsible for the shell prompt.

Check whether it is installed:

```bash
starship --version
```

If you need to install it on another machine, install Starship using its current official installation method.

After installation, verify:

```bash
starship --version
```

---

# 8. Starship Configuration Location

The Starship configuration file is:

```text
~/.config/starship.toml
```

In Git Bash this corresponds to your Windows user directory.

Open it with:

```bash
nano ~/.config/starship.toml
```

You can also edit it using VS Code:

```bash
code ~/.config/starship.toml
```

if the `code` command is available.

---

# 9. Initialize Starship in Bash

Open:

```bash
nano ~/.bashrc
```

Add:

```bash
eval "$(starship init bash)"
```

After saving:

```bash
source ~/.bashrc
```

Verify that the Starship prompt appears.

---

# 10. Starship Directory Configuration

A typical directory section:

```toml
[directory]
style = "bold cyan"
truncation_length = 3
truncate_to_repo = false
```

The directory module shows your current working directory.

For example:

```text
~/Desktop/fahimchowdhury-backend
```

`truncation_length` controls how many directory components are displayed.

---

# 11. Git Branch Configuration

Our configuration:

```toml
[git_branch]
symbol = " "
style = "bold purple"
```

This produces something like:

```text
on  development-draft-one
```

The `` is the branch icon.

---

# 12. Git Status Configuration

Our customized configuration:

```toml
[git_status]
format = '[$all_status$ahead_behind]($style) '
style = "bold red"

modified = " "
untracked = " "
staged = " "
deleted = " "
renamed = " "
conflicted = " "
ahead = "⇡ "
behind = "⇣ "
diverged = "⇕ "
```

This replaces Starship's default:

```text
[!?]
```

with meaningful icons.

## Git status meanings

```text

```

Modified file.

```text

```

Untracked file.

```text

```

Staged file.

```text

```

Deleted file.

```text

```

Renamed file.

```text

```

Merge conflict.

```text
⇡
```

Local branch is ahead of remote.

```text
⇣
```

Local branch is behind remote.

```text
⇕
```

Branch has diverged from remote.

For example:

```text
 
```

means:

```text
modified files + untracked files
```

You can always verify the exact state with:

```bash
git status
```

---

# 13. Node.js Configuration

Our Node.js configuration:

```toml
[nodejs]
symbol = " "
style = "bold green"
format = "[$symbol$version]($style) "
```

Example:

```text
 v22.17.0
```

It appears when Starship detects a Node.js project/environment.

---

# 14. Python Configuration

Our Python configuration:

```toml
[python]
symbol = " "
style = "bold yellow"
format = "[$symbol$version]($style) "
```

Example:

```text
 v3.14.7
```

---

# 15. Docker Configuration

Our Docker configuration:

```toml
[docker_context]
symbol = " "
style = "bold blue"
format = "[$symbol$context]($style) "
```

Example:

```text
 default
```

The Docker context is displayed when applicable.

---

# 16. Command Duration

Our configuration:

```toml
[cmd_duration]
min_time = 2000
format = " [$duration](yellow) "
```

`2000` means 2000 milliseconds = 2 seconds.

Therefore:

```bash
ls
```

normally won't show a duration.

A command that takes more than two seconds can display:

```text
 3.2s
```

This keeps the prompt clean while still showing useful performance information.

---

# 17. Prompt Character

Our prompt character configuration:

```toml
[character]
success_symbol = "[❯](bold green)"
error_symbol = "[❯](bold red)"
```

The prompt looks like:

```text
❯
```

Instead of the default:

```text
>
```

The color changes depending on whether the previous command succeeded or failed.

---

# 18. Removing Starship Fill Dots

If the prompt contains:

```text
........................................
```

those dots may come from:

```toml
$fill\
```

inside the main Starship `format`.

For example:

```toml
format = """
$directory\
...
$fill\
...
"""
```

Remove:

```toml
$fill\
```

if you want a simple one-line prompt without the dotted filler.

---

# 19. Example Starship Prompt

The resulting prompt can look like:

```text
fahimchowdhury-backend on  development-draft-one    v22.17.0
❯
```

This gives you useful information without flooding the terminal with unnecessary information.

---

# 20. zoxide

zoxide is a smarter replacement for repeatedly typing long `cd` commands.

Check installation:

```bash
zoxide --version
```

Example:

```text
zoxide 0.10.0
```

---

# 21. Enable zoxide in Bash

Add this to:

```text
~/.bashrc
```

```bash
eval "$(zoxide init bash)"
```

Only add it **once**.

Do not accidentally create:

```bash
eval "$(zoxide init bash)"
eval "$(zoxide init bash)"
```

After changing it:

```bash
source ~/.bashrc
```

Verify:

```bash
type z
```

You should see something similar to:

```text
z is a function
```

---

# 22. Using zoxide

Add a directory:

```bash
zoxide add ~/Desktop
```

Then:

```bash
z Desktop
```

zoxide remembers directories you visit and lets you jump to them using shorter queries.

Instead of:

```bash
cd ~/Desktop/projects/client/backend
```

you can eventually use:

```bash
z backend
```

when zoxide has learned that location.

---

# 23. Interactive zoxide + fzf

The command:

```bash
zi
```

provides interactive directory selection.

It becomes particularly useful after fzf integration.

---

# 24. fzf

fzf is a fuzzy finder.

Check installation:

```bash
fzf --version
```

Example:

```text
0.74.4
```

---

# 25. Enable fzf Bash Integration

Modern fzf provides its own Bash integration.

Check:

```bash
fzf --bash
```

This outputs the integration scripts.

Add this to:

```text
~/.bashrc
```

```bash
source <(fzf --bash)
```

Then reload:

```bash
source ~/.bashrc
```

Do not use old Linux instructions such as:

```bash
/usr/share/fzf/key-bindings.bash
```

if that directory does not exist on your Windows installation.

The built-in:

```bash
fzf --bash
```

integration is the appropriate approach here.

---

# 26. fzf Shortcuts

## Ctrl + R

Press:

```text
Ctrl + R
```

This opens fuzzy history search.

Instead of remembering the exact command you previously typed, search for part of it.

For example, type:

```text
docker
```

and fzf can find previous Docker commands.

---

## Ctrl + T

Press:

```text
Ctrl + T
```

This opens fuzzy file/directory selection.

Useful when you know part of a filename but don't remember its exact path.

---

## Alt + C

Press:

```text
Alt + C
```

This opens an interactive directory selector.

---

# 27. Git Aliases

The goal is to make frequent Git commands shorter.

Configured aliases:

```bash
git s
git co
git br
git cm
git ps
git pl
git lg
```

The configuration:

```bash
git config --global alias.s status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.cm 'commit -m'
git config --global alias.ps push
git config --global alias.pl pull
git config --global alias.lg 'log --oneline --graph --decorate --all'
```

---

# 28. Git Alias Examples

Instead of:

```bash
git status
```

use:

```bash
git s
```

Instead of:

```bash
git branch
```

use:

```bash
git br
```

Instead of:

```bash
git checkout
```

use:

```bash
git co
```

Instead of:

```bash
git commit -m "fix login"
```

use:

```bash
git cm "fix login"
```

Instead of:

```bash
git push
```

use:

```bash
git ps
```

Instead of:

```bash
git pull
```

use:

```bash
git pl
```

Instead of:

```bash
git log --oneline --graph --decorate --all
```

use:

```bash
git lg
```

---

# 29. Additional Git Shell Aliases

We also added:

```bash
alias gac='git add . && git commit'
alias gca='git commit --amend'
alias gps='git push'
alias gpl='git pull'
alias gcl='git clone'
alias gd='git diff'
alias gst='git stash'
alias gsp='git stash pop'
```

These are **Bash aliases**, not Git aliases.

---

# 30. Git Shell Alias Examples

Stage everything and commit:

```bash
gac "fix authentication"
```

Push:

```bash
gps
```

Pull:

```bash
gpl
```

Clone:

```bash
gcl https://github.com/user/project.git
```

View differences:

```bash
gd
```

Stash:

```bash
gst
```

Restore stash:

```bash
gsp
```

Amend the previous commit:

```bash
gca
```

Be careful with:

```bash
gca
```

because `git commit --amend` changes the previous commit.

---

# 31. Directory Listing Aliases

We added:

```bash
alias ll='ls -lah --color=auto'
alias la='ls -A --color=auto'
alias l='ls -CF --color=auto'
```

Reload after changing `.bashrc`:

```bash
source ~/.bashrc
```

---

# 32. Directory Listing Shortcuts

Detailed listing:

```bash
ll
```

Shows:

* hidden files
* permissions
* sizes
* dates
* directories

Show almost everything:

```bash
la
```

Compact listing:

```bash
l
```

---

# 33. Python Shortcuts

Configured:

```bash
alias py='python'
alias pip='python -m pip'
```

Therefore:

```bash
py --version
```

is equivalent to:

```bash
python --version
```

And:

```bash
pip install package
```

actually executes:

```bash
python -m pip install package
```

Using:

```bash
python -m pip
```

helps ensure that pip belongs to the Python interpreter you're using.

---

# 34. npm Shortcuts

Configured:

```bash
alias ni='npm install'
alias nid='npm install --save-dev'
alias nr='npm run'
alias nrd='npm run dev'
```

Examples:

```bash
ni
```

=

```bash
npm install
```

---

```bash
nid eslint
```

=

```bash
npm install --save-dev eslint
```

---

```bash
nr build
```

=

```bash
npm run build
```

---

```bash
nrd
```

=

```bash
npm run dev
```

---

# 35. uv Shortcuts

Configured:

```bash
alias uvv='uv venv'
alias uvr='uv run'
```

Create a virtual environment:

```bash
uvv
```

Run a command through uv:

```bash
uvr python main.py
```

Equivalent to:

```bash
uv run python main.py
```

---

# 36. Complete .bashrc

Your `.bashrc` should contain the important integrations and aliases.

A conceptual version is:

```bash
# Starship
eval "$(starship init bash)"

# zoxide
eval "$(zoxide init bash)"

# fzf
source <(fzf --bash)

# Directory shortcuts
alias ll='ls -lah --color=auto'
alias la='ls -A --color=auto'
alias l='ls -CF --color=auto'

# Python
alias py='python'
alias pip='python -m pip'

# npm
alias ni='npm install'
alias nid='npm install --save-dev'
alias nr='npm run'
alias nrd='npm run dev'

# uv
alias uvv='uv venv'
alias uvr='uv run'

# Git workflow
alias gac='git add . && git commit'
alias gca='git commit --amend'
alias gps='git push'
alias gpl='git pull'
alias gcl='git clone'
alias gd='git diff'
alias gst='git stash'
alias gsp='git stash pop'
```

Your actual file may contain other Git Bash configuration generated by Git for Windows. **Do not delete that generated configuration just to match this example.**

---

# 37. Git Bash .bash_profile

Git for Windows may create:

```text
~/.bash_profile
```

with:

```bash
# generated by Git for Windows
test -f ~/.profile && . ~/.profile
test -f ~/.bashrc && . ~/.bashrc
```

This is normal.

Do not remove it.

It ensures that `.bashrc` is loaded when Git Bash starts.

---

# 38. Reloading Configuration

Whenever you change `.bashrc`, run:

```bash
source ~/.bashrc
```

You do not need to restart Windows.

You can also completely restart Hyper if necessary.

---

# 39. Finding Your Aliases

To inspect Bash aliases:

```bash
alias
```

To find a specific alias:

```bash
alias ll
```

or:

```bash
alias nrd
```

---

# 40. Finding Git Aliases

Run:

```bash
git config --global --get-regexp '^alias\.'
```

This displays all configured Git aliases.

---

# 41. Checking Starship Configuration

To inspect your Starship config:

```bash
cat ~/.config/starship.toml
```

To edit:

```bash
nano ~/.config/starship.toml
```

---

# 42. Checking Starship Version

```bash
starship --version
```

---

# 43. Checking zoxide

```bash
zoxide --version
```

---

# 44. Checking fzf

```bash
fzf --version
```

---

# 45. Checking Git

```bash
git --version
```

---

# 46. Checking Node.js

```bash
node --version
```

and:

```bash
npm --version
```

---

# 47. Checking Python

```bash
python --version
```

If Python is managed through uv, also:

```bash
uv python list
```

---

# 48. Important Terminal Shortcuts

## Shell / fzf

| Shortcut   | Action                       |
| ---------- | ---------------------------- |
| `Ctrl + R` | Fuzzy search command history |
| `Ctrl + T` | Fuzzy file/directory search  |
| `Alt + C`  | Fuzzy directory navigation   |

## Common terminal navigation

| Command     | Purpose                |
| ----------- | ---------------------- |
| `pwd`       | Show current directory |
| `ls`        | List files             |
| `ll`        | Detailed listing       |
| `la`        | Show hidden files      |
| `l`         | Compact listing        |
| `cd folder` | Enter directory        |
| `cd ..`     | Go one directory up    |
| `cd ~`      | Go to home directory   |
| `clear`     | Clear terminal         |
| `history`   | Show command history   |

## zoxide

| Command           | Purpose                         |
| ----------------- | ------------------------------- |
| `z name`          | Jump to remembered directory    |
| `zi`              | Interactive directory selection |
| `zoxide query`    | Query zoxide database           |
| `zoxide add PATH` | Add directory manually          |

---

# 49. Common Git Commands

| Command            | Purpose                     |
| ------------------ | --------------------------- |
| `git s`            | Status                      |
| `git br`           | Branch list                 |
| `git co`           | Checkout                    |
| `git cm "message"` | Commit                      |
| `git ps`           | Push                        |
| `git pl`           | Pull                        |
| `git lg`           | Graphical-style compact log |
| `gd`               | Git diff                    |
| `gst`              | Git stash                   |
| `gsp`              | Git stash pop               |
| `gcl`              | Git clone                   |
| `gps`              | Push                        |
| `gpl`              | Pull                        |

---

# 50. Common Node.js Commands

| Shortcut   | Original                 |
| ---------- | ------------------------ |
| `ni`       | `npm install`            |
| `nid`      | `npm install --save-dev` |
| `nr build` | `npm run build`          |
| `nrd`      | `npm run dev`            |

---

# 51. Common Python / uv Commands

| Shortcut | Original        |
| -------- | --------------- |
| `py`     | `python`        |
| `pip`    | `python -m pip` |
| `uvv`    | `uv venv`       |
| `uvr`    | `uv run`        |

---

# 52. How to Change the Prompt Icon

Current configuration:

```toml
[character]
success_symbol = "[❯](bold green)"
error_symbol = "[❯](bold red)"
```

You can change:

```text
❯
```

to another symbol.

Examples:

```text
❯
➜
→
»
›
```

For example:

```toml
[character]
success_symbol = "[➜](bold green)"
error_symbol = "[➜](bold red)"
```

Then:

```bash
source ~/.bashrc
```

---

# 53. How to Change the Git Branch Icon

Current:

```toml
[git_branch]
symbol = " "
style = "bold purple"
```

Change:

```text

```

to another icon if desired.

---

# 54. How to Change Node Icon

Current:

```toml
[nodejs]
symbol = " "
```

For example:

```toml
[nodejs]
symbol = "⬢ "
```

The symbol can be changed without changing the Node.js functionality.

---

# 55. How to Change Python Icon

Current:

```toml
[python]
symbol = " "
```

Change the symbol if you prefer another style.

---

# 56. How to Change Git Status Icons

Current:

```toml
modified = " "
untracked = " "
staged = " "
deleted = " "
renamed = " "
conflicted = " "
```

These are purely visual.

The underlying Git status does not change.

---

# 57. How to Add Another Starship Module

Starship modules use sections like:

```toml
[module_name]
...
```

Examples include:

```text
[username]
[hostname]
[time]
[battery]
[cmd_duration]
[docker_context]
[nodejs]
[python]
[git_branch]
[git_status]
```

You can add modules when they provide information you actually need.

Avoid adding every available module. A developer prompt becomes less useful when it becomes visually overloaded.

---

# 58. Troubleshooting Starship

If the prompt suddenly disappears:

```bash
source ~/.bashrc
```

Then check:

```bash
starship --version
```

Check initialization:

```bash
grep -n "starship init" ~/.bashrc
```

You should have one initialization line:

```bash
eval "$(starship init bash)"
```

---

# 59. Troubleshooting zoxide

Check:

```bash
zoxide --version
```

Then:

```bash
type z
```

It should show that `z` is a function.

Check `.bashrc`:

```bash
grep -n "zoxide init" ~/.bashrc
```

There should only be one:

```bash
eval "$(zoxide init bash)"
```

Do not add it twice.

---

# 60. Troubleshooting fzf

Check:

```bash
fzf --version
```

Check integration:

```bash
fzf --bash
```

Check `.bashrc`:

```bash
grep -n "fzf --bash" ~/.bashrc
```

You should have:

```bash
source <(fzf --bash)
```

Then:

```bash
source ~/.bashrc
```

Test:

```text
Ctrl + R
Ctrl + T
Alt + C
```

---

# 61. Troubleshooting Git Aliases

If:

```bash
git s
```

doesn't work, check:

```bash
git config --global --get-regexp '^alias\.'
```

If an alias is wrong, remove it:

```bash
git config --global --unset alias.s
```

Then recreate it.

---

# 62. Troubleshooting Bash Aliases

Check:

```bash
alias
```

For example:

```bash
alias nrd
```

If you modified `.bashrc` but the command isn't available:

```bash
source ~/.bashrc
```

---

# 63. Important Rule When Editing .bashrc

Don't repeatedly append the same configuration using commands such as:

```bash
echo 'something' >> ~/.bashrc
```

without checking first.

Otherwise you can accidentally create duplicates such as:

```bash
eval "$(zoxide init bash)"
eval "$(zoxide init bash)"
eval "$(zoxide init bash)"
```

Instead, inspect:

```bash
nano ~/.bashrc
```

or:

```bash
grep -n "zoxide" ~/.bashrc
```

---

# 64. Recommended Daily Workflow

A typical project workflow becomes:

```bash
cd ~/projects
```

Use zoxide when appropriate:

```bash
z my-project
```

Check Git:

```bash
git s
```

Install dependencies:

```bash
ni
```

Start development:

```bash
nrd
```

For Python:

```bash
uvr python main.py
```

Check changes:

```bash
gd
```

Stage and commit:

```bash
gac "implement authentication"
```

Push:

```bash
gps
```

Search previous commands:

```text
Ctrl + R
```

Find a file:

```text
Ctrl + T
```

Navigate directories interactively:

```text
Alt + C
```

---

# 65. Final Verification Checklist

After setting up a new Windows machine, verify these one by one.

### Terminal

```bash
echo $SHELL
```

Expected:

```text
/usr/bin/bash
```

### Git

```bash
git --version
```

### Starship

```bash
starship --version
```

### zoxide

```bash
zoxide --version
```

### fzf

```bash
fzf --version
```

### Node

```bash
node --version
```

### npm

```bash
npm --version
```

### Python

```bash
python --version
```

### uv

```bash
uv --version
```

### Font

```bash
printf '\ue61c\n'
```

If the icon renders correctly, Cascadia Code PL is working.

### zoxide

```bash
type z
```

### Git aliases

```bash
git s
```

### fzf

Press:

```text
Ctrl + R
```

```text
Ctrl + T
```

```text
Alt + C
```

---

# 66. Final .bashrc Concept

The important custom portion should look approximately like:

```bash
# Starship
eval "$(starship init bash)"

# zoxide
eval "$(zoxide init bash)"

# fzf
source <(fzf --bash)

# Directory
alias ll='ls -lah --color=auto'
alias la='ls -A --color=auto'
alias l='ls -CF --color=auto'

# Python
alias py='python'
alias pip='python -m pip'

# Node / npm
alias ni='npm install'
alias nid='npm install --save-dev'
alias nr='npm run'
alias nrd='npm run dev'

# uv
alias uvv='uv venv'
alias uvr='uv run'

# Git
alias gac='git add . && git commit'
alias gca='git commit --amend'
alias gps='git push'
alias gpl='git pull'
alias gcl='git clone'
alias gd='git diff'
alias gst='git stash'
alias gsp='git stash pop'
```

Keep Git for Windows' generated `.bash_profile` intact.

---

# 67. Final Starship Configuration Reference

The important customized sections are:

```toml
[directory]
style = "bold cyan"
truncation_length = 3
truncate_to_repo = false

[git_branch]
symbol = " "
style = "bold purple"

[git_status]
format = '[$all_status$ahead_behind]($style) '
style = "bold red"

modified = " "
untracked = " "
staged = " "
deleted = " "
renamed = " "
conflicted = " "
ahead = "⇡ "
behind = "⇣ "
diverged = "⇕ "

[nodejs]
symbol = " "
style = "bold green"
format = "[$symbol$version]($style) "

[python]
symbol = " "
style = "bold yellow"
format = "[$symbol$version]($style) "

[docker_context]
symbol = " "
style = "bold blue"
format = "[$symbol$context]($style) "

[cmd_duration]
min_time = 2000
format = " [$duration](yellow) "

[character]
success_symbol = "[❯](bold green)"
error_symbol = "[❯](bold red)"
```

Your top-level `format` should **not contain `$fill\`** if you want to avoid the dotted filler.

---

# 68. Most Important Commands to Remember

If you don't remember anything else, remember these:

```bash
source ~/.bashrc
```

Reload Bash configuration.

```bash
nano ~/.bashrc
```

Edit shell configuration.

```bash
nano ~/.config/starship.toml
```

Edit Starship configuration.

```bash
git s
```

Git status.

```bash
z project
```

Jump to a directory.

```text
Ctrl + R
```

Search command history.

```text
Ctrl + T
```

Find files.

```text
Alt + C
```

Find directories.

```bash
nrd
```

Start an npm development server.

```bash
uvr python main.py
```

Run Python through uv.

---

# 69. Philosophy of the Setup

The purpose of this configuration is not to create the largest possible `.bashrc`.

The goal is:

```text
Fast
+
Readable
+
Predictable
+
Useful information
+
Minimal typing
```

Every alias or prompt element should have a reason to exist.

If something makes the terminal harder to understand, remove it.

The most important parts of this setup are:

```text
Hyper
↓
Git Bash
↓
Starship
↓
zoxide
↓
fzf
↓
Git aliases
↓
Project-specific shortcuts
```

This gives you a lightweight Windows development environment without requiring a Linux VM or WSL just to get a productive terminal experience.
