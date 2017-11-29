# A minimalist guide to tmux

Let’s say you’re using
[vim](https://medium.com/@peterxjang/how-to-learn-vim-a-four-week-plan-cd8b376a9b85)
to edit code on a remote computer [using
ssh](https://medium.com/@peterxjang/web-development-on-an-ipad-69f253bc9c38),
and you want to open a new terminal tab to start a development server. When you
open a new tab, it won’t be connected to the remote machine, which means you
would have to ssh and navigate to the appropriate directory each time.
Furthermore, if your internet connection ever drops, you’ll lose all your ssh
sessions and have to start everything up again.

You can solve these issues by using [tmux](https://github.com/tmux/tmux/wiki), a
command line tool which provides the following key features:

* Enables multiple windows and panes within a single terminal window
* Keeps windows and panes in a session (which stays alive even when the internet
disconnects)
* Enables session sharing (great for pair programming)

### Getting started

To install tmux, you can run `sudo apt-get install tmux` on Linux with
[apt-get](https://help.ubuntu.com/community/AptGet/Howto) or `brew install tmux`
on a Mac with [homebrew](https://brew.sh/). Once it’s installed, you can create
a new tmux session simply by running:

    $ tmux

![](https://cdn-images-1.medium.com/max/1600/1*Ml8e-M7seNIwHBOEN6wOrw.png)

This looks pretty much identical to the regular terminal, except there’s the
green status bar at the bottom. From here we can start running tmux commands to
manage terminal windows and sessions.

### Essential tmux commands

Once you’re in tmux, you can run a command by entering a **prefix key** followed
by a **command key**. By default, tmux uses `Ctrl b` as the prefix key. Note
that you must let go of the prefix before entering the command key.

There are many tmux commands available, but here are the only ones you need to
get started:

    <prefix> c: Create a new window (appears in status bar)

    <prefix> 0: Switch to window 0

    <prefix> 1: Switch to window 1

    <prefix> 2: Switch to window 2 (etc.)

    <prefix> x: Kill current window

    <prefix> d: Detach tmux (exit back to normal terminal)

If you kill all the windows in a tmux session, it will kill the overall session
and return you to the normal terminal. If you use `<prefix> d` to detach tmux,
you’ll be back in the normal terminal with your tmux session still running in
the background. To see all tmux sessions, you can enter:

    $ tmux ls

To attach to the last used session, you can enter:

    $ tmux a

To attach to a specific session, you can enter:

    $ tmux a -t <session-name>

And that’s it! Now you’re able to work on remote computers with multiple
terminal windows and persistent sessions. You can even pair programming by
having two people attach to the same tmux session!

### Next steps

The above commands are truly all you need to take advantage of the most
important features of tmux. I try to keep things minimal, with one window for my
text editor (vim), another window for a development server, and a third window
for running any other commands.

Most people using tmux tend to use panes, which allows for multiple terminal
views within a single window. You can do some crazy customizations with panes:

![](https://cdn-images-1.medium.com/max/1600/1*ZVmiTfLBYpTUdh-Tadx_SQ.png)
<span class="figcaption_hack">From
[reddit.com/r/unixporn](https://www.reddit.com/r/unixporn/comments/689wfd/tmux_the_bridge/)</span>

Panes are definitely cool and can be worth learning, but I would recommend
holding off on them to start off to reduce the learning curve of tmux. When you
use panes, you’ll need to memorize commands to create panes vertically and
horizontally, navigate between panes, resize panes, destroy panes, etc. It will
more than double the number of commands you need to memorize to get started! I
would use tmux without panes for at least a week or two before trying out a new
set of commands.

You can also customize tmux by making a `.tmux.conf` file in your home
directory. Some common customizations include changing the prefix to `Ctrl a` (a
little faster to type, doesn’t conflict with vim), start window numbering at 1
instead of 0 (again, a little faster to type), and customizing colors. If you
are planning on rebinding the prefix key, then you should probably do that first
so you build the right muscle memory. Here’s an absolutely minimal `.tmux.conf`
file to change the prefix and window numbering:

    bind-key C-a send-prefix

    # Start window numbering at 1
    set -g base-index 1

Again, tmux has a large number of options you can configure here, but to get
started you want to keep it as minimal as possible. And once you’re ready to try
out advanced features, don’t just blindly paste configurations you find online.
It’s important that you understand each line you add to your `.tmux.conf` file!

Once you feel like you’ve mastered the basics, there are a ton of great
resources out there to take your tmux game to the next level. However, to
paraphrase Dr. Ian Malcolm, don’t be so preoccupied with whether or not you
could that you don’t stop and think if you should. I would argue you get more
than 80% of tmux’s advantages using the above minimal set of commands and
customizations. Hope you find these tips useful on your journey!
