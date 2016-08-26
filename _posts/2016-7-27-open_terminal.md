---
layout: post
title: Tutorial: How to open Terminal in a folder from OSX
published: True
---

This post will show you how to create a feature in OSX where you right click on a file, and it opens a Terminal in the containing folder.  After some searching, I found out that you can do this with Automator.  I found instructions [here](http://www.macworld.com/article/1047793/folderinterm.html) but they were out of date and some of the relevant pieces of Automator have changed.  So I wrote an updated version.  

There is a method for doing this built into OSX, which you can [enable](http://www.howtogeek.com/210147/how-to-open-terminal-in-the-current-os-x-finder-location) , but it works in different circumstances.  The built-in Service only works when you right-click a folder, while this method will work on files and forlders.  Also, it can be customized to do special actions when it executes.  For instance, if you uncomment a line in the code in this example, it will run `ls`.

1. Create a new automator and select "Service" for the type.
{% include image.html url="/assets/open_terminal/select_service1.png" description="Select Service" %}

2. Now you need to set the context where this Service will run.  In the bar at the top of the window, click the menu titled "Service receives selected" and pick "files or folders".  Then click the "in" menu and choose "Finder"
{% include image.html url="/assets/open_terminal/context2.png" description="Set up the service to run on files and folers in Finder" %}

3. Choose "Files & Folders" from the Actions menu, and then pick "Get Selected Finder Items" and drag it into the work area on the right.
{% include image.html url="/assets/open_terminal/workspace1.png" description="Add Get Selected Files and Folders item" %}

4. Now choose "Utilities" from the Actions menu, and drag "Run Applescript" from the right column into the work area below the last thing you put there.
{% include image.html url="/assets/open_terminal/workspace3.png" description="Add AppleScript item" %}

5. Now you need to add code to the AppleScript block in the workspace.  Copy this code, replacing everything that's currently there.
{% include image.html url="/assets/open_terminal/workspace4.png" description="Add code" %}

```
on run {input, parameters}
    tell application "Finder"
        set myWin to window 1
        set theWin to (quoted form of POSIX path of (target of myWin as alias))
        tell application "Terminal"
            activate
            tell window 1
                do script "cd " & theWin
                -- do script "cd " & theWin & ";ls -al | more"
            end tell
        end tell
    end tell
    return input
end run
```

Now save it with a descriptive name, because the name of this file will determine what your new service is called.
{% include image.html url="/assets/open_terminal/save.png" description="Save it with a descriptive name" %}

{% include image.html url="/assets/open_terminal/finder2.png" description="Now your service shows up in finder" %}

If you need to find this file, it's located in `~/Library/Services`.  It's a hidden directory so I opened it by doing the reverse of the action we just created.  Open the directory in the Terminal, and type `open .` to open a finder window at that location.
