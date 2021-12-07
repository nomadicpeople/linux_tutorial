# Tmux

- In this section we will go the installation and basic usage of Tmux to get you up and running. 

- Tmux is a terminal multiplexer an alternative to GNU Screen. In other words, it means that you can start a Tmux session and then open multiple windows inside that session. Each window occupies the entire screen and can be split into rectangular panes.

- With Tmux you can easily switch between multiple programs in one terminal, detach them and reattach them to a different terminal.

- Tmux sessions are persistent, which means that programs running in Tmux will continue to run even if you get disconnected.

- Tmux has been installed on all of the ISSAI servers. If you would like to install and experiment with Tmux on your local machine, we refer you to this [post](https://linuxize.com/post/getting-started-with-tmux/). 

 #### Starting Your First Tmux Session
 To start your first Tmux session, simply type **`tmux`** in your console:
 ```
 tmux
 ```
 This will open a new session, create a new window, and start a shell in that window.

 Once you are in Tmux you’ll notice a status line at the bottom of the screen which shows information about the current session.

 You can now run your first Tmux command. For example, to get a list of all commands, you would type:
 ```
 Ctrl+b ?
 ```
 #### Creating Named Tmux Sessions
 By default, Tmux sessions are named numerically. Named sessions are useful when you run multiple Tmux sessions. To create a new named session, run the tmux command with the following arguments:
 ```
 tmux new -s session_name
 ```
 It’s always a good idea to choose a descriptive session name.
 #### Detaching from Tmux Session
 You can detach from the Tmux session and return to your normal shell by typing:
 ```
 Ctrl+b d
 ```
 The program running in the Tmux session will continue to run after you detach from the session.

 #### Re-attaching to Tmux Session
 To attach to a session first, you need to find the name of the session. To get a list of the currently running sessions type:
 ```
 tmux ls
 ```
 The name of the session is the first column of the output.
 ```
 0: 1 windows (created Sat Sep 15 09:38:43 2018) [158x35]
 my_named_session: 1 windows (created Sat Sep 15 10:13:11 2018) [78x35]
 ```

 As you can see from the output, there are two running Tmux sessions. The first one is named 0 and the second one my_named_session.
 For example, to attach to session 0, you would type:
 ```
 tmux attach-session -t 0
 ```
 #### Working with Tmux Windows and Panes

 When you start a new Tmux session, by default, it creates a single window with a shell in it.

 To create a new window with shell type ```Ctrl+b c```, the first available number from the range 0...9 will be assigned to it.

 A list of all windows is shown on the status line at the bottom of the screen.

 Below are some most common commands for managing Tmux windows and panes:

 - ```Ctrl+b c```Create a new window (with shell)

 - ```Ctrl+b w``` Choose window from a list

 - ```Ctrl+b 0 ```Switch to window 0 (by number )

 - ```Ctrl+b ,``` Rename the current window

 - ```Ctrl+b %``` Split current pane horizontally into two panes

 - ```Ctrl+b "```Split current pane vertically into two panes

 - ```Ctrl+b o```Go to the next pane

 - ```Ctrl+b ;``` Toggle between the current and previous pane

 - ```Ctrl+b x``` Close the current pane

 #### Basic Tmux Usage

 Below are the most basic steps for getting started with Tmux:

 01. On the command prompt, type tmux new -s my_session,

 02.  Run the desired program.

 03. Use the key sequence Ctrl-b + d to detach from the session.

 04. Reattach to the Tmux session by typing tmux attach-session -t my_session.


References:
1. https://linuxize.com/post/getting-started-with-tmux/

