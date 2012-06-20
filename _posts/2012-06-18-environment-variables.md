---
layout: post
title: "Environment Variables"
tagline: "and the PATH"
category: [tutorials]
tags: [software, tutorial]
---
{% include JB/setup %}
A lot of times when you install something, it will tell you to add `"some/path/bin"` to your `PATH` environment variable.
Sometimes they tell you to create a new one called `EXAMPLE_HOME` or something like that. These instructions will first go through explaining how to set environment variables in addition to explaining the `PATH` variable as it's the most commonly used one.

These instructions are for Windows 7, though I believe the instructions should work for Vista as well.

###Change an environment variable

1. Open an Explorer window (Hotkey: Win+E) and click `System properties`
    {% assign image_id = "10" %}
    {% include image %}

2. In the left column, click `Advanced System settings`
    {% assign image_id = "20" %}
    {% include image %}

3. Click the `Environment Variables...` button.

4. This is the screen that allows you to create, modify, and delete environment variables. The section on top is only for you, while the system variables affect all users. The `PATH` variable is a system variable.
    {% assign image_id = "60" %}
    {% include image %}
- - -

###Explaining the PATH variable
Walk through (or just read) the following steps to see what the `PATH` variable does.

1. Open a text editor and create a file named `madness.bat` with the following contents:
        
        @echo off
        echo "Madness? This. is. SPARTA!"
2. Create a folder called `sparta` on the `C:\` drive.
3. Save `madness.bat` in the folder `C:\sparta`.
4. Open a terminal/command prompt and enter the command: `madness`. This causes an error

        C:\Users\Talon>madness
        'madness' is not recognized as an internal or external command,
        operable program or batch file.

    {% assign image_id = "30" %}
    {% include image %}

5. So what gives? It's definitely a batch file. Well, you might say "Obviously it won't work, you're not giving it the full path." Ok so lets see what happens when we fix that. Enter the command `C:\sparta\madness.bat`.
    
        C:\Users\Talon>C:\sparta\madness.bat
        "Madness? This. is. SPARTA!"
    _Note: If your path has spaces, you must surround the path with quotes_

    Ok so it worked, but I don't want to type the path everytime. Let's fix that with the %PATH% variable.

6. Review the instructions in the first section of this post and at the Environment Variables screen, scroll through the `System variables` and find the variable named `PATH`.
7. Click `Edit...` and a window will pop up allowing you to edit the variable value.
8. **Warning!** &mdash; Do not erase anything currently in the Variable value textfield or you might make certain programs not work.

    We must edit the `PATH` variable to include the path to our folder we created in step 2. 
    To do this, at the very end of the text in the `Variable value` textfield, there should be a semicolon.
    If there isn't one, add one. The semicolon is what separates the paths. 
    Edit your path variable value by appending `;C:\sparta;` to it. The semicolons are precautionary,
    if there was already a semicolon at the end of your Variable value, you don't need to include the one before the path.
    I usually add a semicolon at the end of paths just so I don't have to do it when I go to add a new one in the future.
    
    {% assign image_id = "40" %}
    {% include image %}

9. Click on `Ok` on all of the dialog boxes to save the changes.
10. Close the command prompt and re-open it so that it loads the new `PATH`
11. Now try entering the command `madness` again.
    As you can see, the command now works.

    {% assign image_id = "50" %}
    {% include image %}

12. That's it! Essentially, the `PATH` variable is what's checked when you enter commands to save you from typing the full path every time. 

####Tips

*  You can find out the value of an environment variable by echoing it surrounded with percent symbols. (Ex: `echo %PATH%`)
*  The environment variable `PATHEXT` dictates what file extensions it will run. You can test it out by changing the extension of madness.bat from a `.bat` to something random like `.lol` then add `;.LOL` to your `PATHEXT` variable. Then restart the command prompt and enter `madness`. Of course, if you don't have anything to handle .lol files, windows will ask what you want to do with that filetype.