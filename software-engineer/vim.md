# How To Learn Vim: A Four Week Plan

Vim with custom color scheme, syntax highlighting, linting, and autocomplete

Vim is a command line text editor that is notorious for being hard to learn (the running joke is to generate a truly random string, put a web developer in front of Vim and tell them to exit). So why bother learning it, especially if you’re already comfortable with your text editor or IDE? Some benefits to learning Vim include:

* **Vim is already installed on any Unix-like system**, which means you can edit files directly on a server (a genuine superpower)

* **Vim is lightweight compared to most text editors and IDEs**, so it runs fast and efficiently on even the most modest hardware

* **Vim is completely keyboard driven** (with most actions centered on the home row), so it will make you more efficient?

I put a question mark on that last one about making you more efficient — it’s an argument you’ll hear often, but I’m not sure it’s true for everyone. Basically, in order to be efficient with Vim, you have to invest a lot of time into not just learning it, but mastering it. Which means the time you save using it is offset by the time you invest mastering it, and you are always investing time mastering it. I would say **the best reason to learn Vim is because you enjoy spending time learning and mastering a complex skill**. In this way it’s not that different from why someone would want to learn a new musical instrument!

If these ideas sound appealing to you, then you can follow the four week plan outlined below to help you learn Vim. This is how I learned Vim, which was based upon the advice that I’ve come across repeatedly in forums and tutorials. I’ve also added some of my own tips that helped me out along the way.

## Week 1: Complete vimtutor once a day, every day

Many people agree that the best way to learn the basics of vim is to simply type this command in your terminal:

    $ vimtutor

This will open up a text file in Vim with step-by-step instructions that cover essential Vim commands. It should take you 30 minutes or so to get through the whole thing. If you know the commands covered in vimututor, you’re pretty much ready to start being productive in Vim.

The problem is that there are a **lot** of commands covered in vimtutor — there is no way you can learn them all from one sitting! My recommendation is to practice deliberately by doing vimtutor once a day for at least one week straight. Each time you do it, see if your time improves. Set a goal for yourself — see if you can get through the whole thing in 5 minutes. **The point isn’t to memorize every single command** — the point is to practice enough times until the basic navigation and editing commands are second nature.

If your goal is to know enough Vim to be able to edit files remotely on a server, you can stop here — you already know enough to be dangerous! If you want to use Vim as your editor of choice, you can continue to the next step.

## Week 2: Use Vim with minimal config, no plugins

Now that you’re comfortable navigating and editing in Vim, you’ll want to configure it to work with your personal workflow. Vim has a pretty bland and outdated default configuration, but it’s easy enough to customize it with modern features using a vimrc configuration file. The key is to not go crazy with plugins to try to make Vim into a full blown IDE — Vim is great at being Vim and bad at being an IDE.

Instead, follow [this article](https://dougblack.io/words/a-good-vimrc.html) to build your own vimrc file. As a starting point, these are the only things I would configure:

* Add a color scheme (I use [vim-code-dark](https://github.com/tomasiser/vim-code-dark), based on Visual Studio Code)

* Turn on syntax highlighting

* Set up spaces and tabs

* Set up auto indentation

* Turn on line numbers

* Find files in subfolders with tab completion (watch this [video](https://www.youtube.com/watch?v=XA2WjJbmmoM&t=408s) for 5 minutes)

* Configure a faster way to hit **ESC** to exit insert mode (I changed my caps lock key to **CTRL** and use **CTRL C** to exit insert mode)

Honestly, that’s it! (The only exception to the no plugins rule is if you need to install language specific support for any languages that Vim doesn’t support out of the box). The goal is to avoid any additional configuration or fancy plugins for a week — this may feel painful, but it will prevent you from spending all your time configuring Vim and none of your time practicing Vim.
> **Pro tip: **when you’re configuring vim, use a .vim folder in your home directory with the following directory structure below (read more details [here](http://www.panozzaj.com/blog/2011/09/09/vim-directory-structure/)). Newer versions of Vim will look for the vimrc file in the .vim folder, so you can keep everything in a single folder. This allows you to make your .vim folder a single git repo that you can easily clone onto any computer!

    .vim/
    ├── colors/   <- directory for color schemes
    ├── plugin/   <- directory for standard plugins
    └── vimrc     <- file with main config

## Week 3: Use Vim with minimal plugins

After you have used Vim for real projects, you’ll have a better sense of what Vim is capable of, and you’ll probably be itching to customize it even further. However, you should still avoid installing plugins that fundamentally change how Vim works. This is a list of popular types of plugins that I recommend you still avoid right now:

* **Avoid installing** a plugin manager (newer versions of Vim handle plugins natively well enough)

* **Avoid installing** a tree explorer or fuzzy file finder plugin (:find with with [subfolder searching](https://www.youtube.com/watch?v=XA2WjJbmmoM&t=408s) works well instead)

* **Avoid installing** a plugin for visual tabs (try to get used to native Vim buffers, :b <TAB> works well here)

* **Avoid installing** a plugin for autocompletion (Vim already can do it natively with <CTRL n>)

* **Avoid installing** a plugin for multi-line comments (try using visual mode instead)

* **Avoid installing** a plugin for multiple cursors (try using a / search with n and . repeated as needed)

The general theme here is that plugins are often a crutch that prevents you from learning Vim’s actual capabilities. All of the above types of plugins are great and may save you time, but you should only install them if you fully understand how to accomplish the same task using “vanilla” Vim.

That being said, there are a few plugins that don’t change Vim’s core behaviors that can make life more convenient. Here are some plugins I use that fall into that category:

* **Consider installing** [auto-pairs.vim](https://github.com/jiangmiao/auto-pairs) (inserts or deletes brackets, parens, quotes in pairs)

* **Consider installing** [endwise.vim](https://github.com/tpope/vim-endwise) (in Ruby, adds end after if, do, def, etc.)

* **Consider installing** [ragtag.vim](https://github.com/tpope/vim-ragtag) (helpers for tags in HTML, erb, etc.)

## Week 4: Compose Vim commands with verbs and nouns

At this point you should know Vim well enough to focus on composing new commands instead of memorizing new ones. To compose new commands, it helps to think of Vim as a language. Chris Toomey’s [Mastering the Vim Language](https://www.youtube.com/watch?v=wlR5gYd6um0) talk is worth watching in its entirety to see how powerful this concept is:

<center><iframe width="560" height="315" src="https://www.youtube.com/embed/wlR5gYd6um0" frameborder="0" allowfullscreen></iframe></center>

In a nutshell, you need to know some verbs and nouns:

* Verbs — **d** (delete), **c** (change), **y** (yank/copy), **> **(indent)

* Nouns (motions) — **w** (word), **b** (back a word), **2j** (down 2 lines)

* Nouns (text objects) — **iw** (inner word), **it** (inner tag), **i”** (inner quotes)

Then you can compose verbs and nouns to create any number of commands:

* **dw** to delete to the end of a word

* **diw** to delete the entire word at the cursor

* **y4j** to copy 4 lines

* **cit** to change the content inside an HTML tag

The talk points out that memorizing about 30 commands gives you the ability to compose over 2,000 distinct commands. Note that I’m putting this in week 4 — this stuff is very empowering, but only once you have a good general grasp of Vim. After 3 weeks you should have a pretty handle on the 30 commands necessary to achieve this level of wizardry!

The talk also mentions installing plugins to add more to the Vim language. As always, you should exercise caution when installing plugins. But in this case, we’re talking about plugins that add to Vim as a language (as opposed to plugins that contradict Vim’s core behaviors). Some plugins worth looking at:

* **Consider installing** [surround.vim](https://github.com/tpope/vim-surround) (adds a new modifier to change surrounding quotes, parentheses, etc.)

* **Consider installing** [commentary.vim](https://github.com/tpope/vim-commentary) (adds a new verb to comment lines)

* **Consider installing** [repeat.vim](https://github.com/tpope/vim-repeat) (adds **.** repeat support for certain plugins)

(All the above plugins are by [Tim Pope](https://github.com/tpope), a name you’ll definitely run across on your journey to mastering Vim).
> **Pro tip**: In the talk they go over using [relative line numbers](https://jeffkreeftmeijer.com/vim-number/), which I actually don’t recommend. A lot of people were big fans when it was first introduced, but I’ve also heard of people having issues with it after a while (harder to read code, sometimes causes performance issues). I personally don’t see the use for it since you can accomplish the same thing (moving or deleting to a specific line) just as easily using regular Vim commands **G** or **gg** (see [here](https://stackoverflow.com/questions/6384561/delete-from-the-current-cursor-position-to-a-given-line-number-in-vi-editor)).

## Conclusion

Learning Vim is a lot of work but can also be a lot of fun. If you recoil at the idea of spending a month to learn a text editor, this may not be for you. However, I do think most developers would benefit from following the advice in week 1 to at least get the superpower of being able to edit files directly on a server. You’ll be able to do amazing things like [truly write code on an iPad](https://medium.com/@peterxjang/web-development-on-an-ipad-69f253bc9c38) or Chromebook using a VPS. At the minimum, you won’t look silly getting stuck in Vim when it randomly opens in your terminal!

If you do spend the time to go through all 4 weeks, then you can take your programmer editing game to a whole other level. I honestly don’t know if it will make you more efficient (since you’ll probably spend the time that you saved writing code on learning more cool tricks and trying new configurations). Again, it’s more like learning a musical instrument — depending on your personality, you can get a real kick out of the process of continually mastering Vim. Hope you find these tips useful on your journey!
