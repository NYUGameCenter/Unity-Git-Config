<div style="align:center"><img src ="https://github.com/NYUGameCenter/Unity-Git-Config/blob/master/NYU_GameCenter_Logo_Formatted_Thin.png"></div>

# Unity Github Config
- [Git Primer](#git-primer)
- [Setup Instructions](#setup-instructions)
- [Usage and Errors](#usage-and-errors)
- [Troubleshooting](#troubleshooting)
- [Additional Information](#additional-information)

We've put together some git configuration files to cover the majority of Unity/Git use cases. If you set these up at the start, they should prevent your repos from filling up with cruft. These config files ensure that all large files are tracked by git lfs & that your changes are diff'd appropriately, while the pre-commit/post-merge hooks ensure that meta files stay properly in sync. They also insure you against accidentally trying to upload a >100mb file to github, and ending up with a sad unresolvable local repo.

This process has 4 phases & some prequisites. Please make sure to complete all phases before starting work on your project.

  0. [Prerequisites](#prerequisites)
  1. [Configure Unity for Git](#configure-unity-for-git)
  2. [Create and Configure Your Repo](#create-and-configure-your-repo)
  3. [Install GitLFS](#install-gitlfs)
  4. [Invite Teammates](#invite-teammates)

# Git Primer

Want a primer on git?

 * [Git, the simple guide](http://rogerdudler.github.io/git-guide/) - A very simple primer
 * [Git Magic](http://www-cs-students.stanford.edu/~blynn/gitmagic/) - A command-oriented, more extensive git primer
 * [Swarthmore Git Intro](https://www.cs.swarthmore.edu/help/git/) - A more conceptually-driven git primer
 
How about a cheatsheet?

 * [Rogerdudler's Cheatsheet](https://rogerdudler.github.io/git-guide/files/git_cheat_sheet.pdf) - Just the essentials, one-pager
 * [GitHub's Cheatsheet](https://services.github.com/on-demand/downloads/github-git-cheat-sheet.pdf) - More extensive, longer descriptions
 * [NDP's Cheatsheet](http://www.ndpsoftware.com/git-cheatsheet.html) - Interactive, even more extensive

# Setup Instructions

## Prerequisites

Unity 2017 or newer. Tested up to Unity 2018.3.

* Mac: Git installed either through Xcode command line tools, or from here: http://git-scm.com/download/mac
* Windows: Git installed using GitForWindows: https://gitforwindows.org/ Note that other windows git installs that don't include gitbash will cause the pre-commit & post-merge hooks to fail, negating many of the key benefits of this setup.
  

## Configure Unity for Git

1. Create a new unity project.

2. Open the editor settings:

   `Edit > Project Settings > Editor`

3. Force visible .meta files (this will ensure script execution order & object references are maintained)

   `Version Control / Mode: “Visible Meta Files”`

4. Force text serialization (this will ensure you can merge & properly diff your assets)

   `Asset Serialization / Mode: “Force Text”`

5. Save changes

   `File > Save Project`

## Create and Configure Your Repo 

1. Create a new github repo with the same name as your Unity project. Don't select the default Unity .gitignore, we'll be importing our own later.

2. Clone the repo to the Unity project folder you created in "Configure Unity for Git".

   >If you can't see the `/.git/` folder, make it visible by following [these steps for Windows](https://kb.wisc.edu/page.php?id=27479) or [these steps for Mac](https://ianlunn.co.uk/articles/quickly-showhide-hidden-files-mac-os-x-mavericks/).

3. Download the .gitconfig, .gitignore,  and .gitattributes file from this into the root of the local repo you just cloned, ie into the folder `<your_repo>/`.

4. Edit .gitconfig with a text editor, replacing `<path to UnityYAMLMerge>` with the location of your Unity install's merge tool (note that these locations can vary if you picked a different install folder during unity install. Also note that you will need to edit this file again if you upgrade Unity & choose a different install location.)
    >On Windows it's usually: `C:\\Program Files\\Unity\\Editor\\Data\\Tools\\UnityYAMLMerge.exe` or `C:\\Program Files (x86)\\Unity\\Editor\\Data\\Tools\\UnityYAMLMerge.exe` (double slashes are necessary as escape characters).  

    >On Mac it's usually: `/Applications/Unity/Unity.app/Contents/Tools/UnityYAMLMerge`.   

   This merge tool will try to merge or resolve conflicts within .prefab, .scene, and other unity asset files. If it can't do it automatically, your default merge tool will open & you can manually select which changes to include.  
   **Always open any merged unity assets & confirm the merge worked before pushing the merged assets.** For more info, check [this git hub post](https://github.com/anacat/unity-mergetool) or [this blog post](http://www.jameskeats.com/blogs/post/Unitys-SmartMerge-Meets-SourceTree/).

5. Copy the contents of your Unity project into the new folder.

6. Commit these changes to your new repo & push. Your new project should look like this on Github:

<div style="align:center"><img src ="https://github.com/NYUGameCenter/Unity-Git-Config/blob/master/testproject.jpg"></div>
(Keep scrolling, you're not done yet!)

## Install GitLFS 

1. Download & install git-lfs from https://git-lfs.github.com/. If you've already installed git-lfs, proceed to step 2.

2. Open a command prompt, terminal, or gitbash window. 

3. Navigate to the folder containing your git repository & execute: `git lfs install`

4. That's all you need to do, as tracking the appropriate files in lfs is taken care of by the .gitattributes file. If you're already familiar with git, you might consider reading [this intro to git-lfs](https://github.com/git-lfs/git-lfs/wiki/Tutorial), as working with it varies from vanilla git quite a bit.

5. Download the [pre-commit](https://github.com/NYUGameCenter/Unity-Git-Config/blob/master/pre-commit) & [post-merge](https://github.com/NYUGameCenter/Unity-Git-Config/blob/master/post-merge) scripts. Enable them in your repo by moving them into the folder `<your_repo>/.git/hooks/`.  These will ensure that meta files stay in sync. It will also alert you if you attempt to commit a >100mb file, which github will reject. It will reject the commit, allowing you to revise it to remove or reduce the size of the offending file(s). **These scripts have to be installed individually on each computer you clone the repo to. Please ensure your teammates have installed these as well.**

## Invite Teammates

1. Make sure they've all installed git lfs!

2. Add them to your repo.

3. Help them clone the repo, copy the `pre-commit` & `post-merge` scripts into `/.git/hooks/`, and setup the .gitconfig file for their system (steps 3-5 of Create & Configure Your Repo).

# Usage and Errors

Now that you have these hooks installed, they'll automatically stop you if you try to commit files that might mess up your project. There are a few ways this can happen.

## Attempt to Commit File >100MB
If you try to commit a file that's bigger than 100MB, you'll see an error like this one:

>Commit failed with error
>			0 files committed, 1 file failed to commit: testing  
 >			`Assets/big.pdf` is over 100MB.  
 >			Can't commit, fix errors first.  

Resolve this error by reducing the size of the file. For audio or visual assets, try splitting them into smaller parts or compressing them. For unity .scene files, try to reduce the scene size by dragging elements out of the scene and into prefabs.

## Failure to Commit Metafile
If you try to commit an asset without a corresponding metafile, you'll see an error like this one:

>Commit failed with error
>			0 files committed, 1 file failed to commit: testing . 
 >			Error: Missing meta file.  
 >			Asset `Assets/LensFlare.flare` is added, but `Assets/LensFlare.flare.meta` is not in the git index.  
 >			Please add `Assets/LensFlare.flare.meta` to git as well.

Resolve this error by adding the corresponding .meta file to your commit.

## Failure to Add Corresponding Metafile to Gitignore

If you add a file or folder to the .gitignore, but don't add the corresponding .meta to your .gitignore, you'll see an error like this one:

>Commit failed with error  
 >			0 files committed, 3 files failed to commit: testing  
 >			`LensFlare.flare`  
 >			`LensFlare.flare` found in .gitignore but not the corresponding meta file! Please add `LensFlare.flare.meta` to .gitignore . 

Resolve this error by editing your .gitignore by adding the .meta file to it.

# Troubleshooting

Did everything above & still managed to run into a problem? Here are some of the best resources for learning how to restore your repo. 

 * [On undoing, fixing, or removing commits in git](https://sethrobertson.github.io/GitFixUm/fixup.html) - A choose-your-own-adventure style troubleshooter
 * [Oh shit, git!](https://ohshitgit.com/) - Lots of common use cases, expressed simply & crassly
 * [10 Common Git Problems](https://www.codementor.io/citizen428/git-tutorial-10-common-git-problems-and-how-to-fix-them-aajv0katd) - Similar to the above, less crass
 * [git-lfs Troubleshooting](https://github.com/git-lfs/git-lfs/wiki/Troubleshooting) - Common issues folks run into while using git-lfs

# Additional Information

Want more info on how we built these config files & hooks? Here's some of the docs & posts we read when building this: 
 
  * http://www.gamasutra.com/blogs/TimPettersen/20161206/286981/The_complete_guide_to_Unity__Git.php 
  * http://www.edwardthomson.com/blog/git_with_unity.html
  * https://riptutorial.com/unity3d/example/7179/setting-up-a-git-repository-for-unity
  * https://thoughtbot.com/blog/how-to-git-with-unity
  * http://teaclipper.co.uk/2016/11/11/the-perfect-unity-git-repo/
  * http://www.jameskeats.com/blogs/post/Unitys-SmartMerge-Meets-SourceTree/
  * https://nagachiang.github.io/tutorial-setup-smart-merge-for-unity-assets-with-git/
  * https://www.forrestthewoods.com/blog/managing_meta_files_in_unity/
