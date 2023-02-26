+++
title = "tmux - walkthrough with a practical example"
date = 2023-02-26

[taxonomies]
categories = ["Linux"]
+++

This brief post contains some notes related to tmux - from installation to practical example.

<!-- more -->

## Docs and installation

- [docs-getting-started](https://github.com/tmux/tmux/wiki/Getting-Started)
	- `sudo apt install tmux`

## Create new session

- Type  `tmux` to initiate new session.

## Create new pane to right side in terminal

- `Ctrl + b` and right after that `%` or percentage sign.
- type `exit` to close the pane.

## Switch between panes

- `Ctrl + b + ← →` - use navigation keys. 

## Create new pane to bottom of the terminal

- `Ctrl + b "` - quotation mark at the end.

## Creating windows

-  `Ctrl + b + c` - creates new window with label 1.
-  To switch back to window 0, type `Ctrl + b + 0`. 

## Renaming windows

- For example, we are working with Git in this window:
	- `Ctrl + b + ,` - comma at the end and type git.

- In second window we are working with Docker, and we will name it:
	- `Ctrl + b + ,` - and type docker.

## Sessions

- The power of `tmux` is that handles our processes in a form of sessions. 
- When we start tmux, we start a tmux session that preserves our state or a process that is running within that window.
- If we lose the connection to SSHed server, but we were using tmux, we can just reload and continue from where we left, if we were running a process - that process would not be terminated.

- To detach the session 0 that we were working on:
	- `Ctrl + b + d`

- To view sessions running in background:
	- `tmux ls`

- To reattach to a session 0:
	- `tmux attach -t 0`

## Practical example

- Practical example where we can see that tmux actually preserves a state:
	- `git config --global --list`
	- we have the output.
- Now let's detach the session:
	- `Ctrl + b + d`
- To see if it's running:
	- `tmux ls`
- To attach back to session and to see that exact state is preserved:
	- `tmux attach -t 0`

## Rename session 0:

- `tmux rename-session -t 0 git`
- `tmux ls` - output will show that session name is called git.
- `Ctrl + l` - to clear the terminal.

## To create a new session and name it before the session starts:

- `tmux new -s docker` - the session will be named 'docker'
- `Ctrl + b + d` - to detach
- `tmux ls` - to list sessions we are running - we can see docker and git.

## To delete or kill sessions we are not using:

- `tmux kill-session -t docker` - kills docker session.
- `tmux ls` - the output will not show docker session.
- `tmux kill-session -t git` - kills git session.

- Keep in mind, if not killed, these sessions will be preserved until system reboots.