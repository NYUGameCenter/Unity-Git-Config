# Unity-Git-Config
We've put together some git configuration files to cover the majority of Unity/Git use cases. If you set these up at the start, they should prevent your repos from filling up with cruft. These config files ensure that all large files are tracked by git lfs & that your changes are diff'd appropriately, while the pre-commit/post-merge hooks ensure that meta files stay properly in sync.

Want more info? Here's some of the posts we refered to when building these: 
  * http://www.gamasutra.com/blogs/TimPettersen/20161206/286981/The_complete_guide_to_Unity__Git.php 
  * http://www.edwardthomson.com/blog/git_with_unity.html
  * https://riptutorial.com/unity3d/example/7179/setting-up-a-git-repository-for-unity
  * https://thoughtbot.com/blog/how-to-git-with-unity
  * http://teaclipper.co.uk/2016/11/11/the-perfect-unity-git-repo/
  * http://www.jameskeats.com/blogs/post/Unitys-SmartMerge-Meets-SourceTree/
  * https://nagachiang.github.io/tutorial-setup-smart-merge-for-unity-assets-with-git/
  * https://www.forrestthewoods.com/blog/managing_meta_files_in_unity/

# Setup instructions:

## First: Create & Configure Your Repo 

1. Create a new github repo.

2. Clone the repo to your local machine.

3. Download the `pre-commit` & `post-merge` scripts. These will ensure that meta files for gitignored files get ignored properly. Enable them in your repo by moving them into the folder `<your_repo>/.git/hooks`.  
>If you can't see the `/.git/` folder, make it visible by following these steps for Windows: https://kb.wisc.edu/page.php?id=27479 or these for Mac: https://ianlunn.co.uk/articles/quickly-showhide-hidden-files-mac-os-x-mavericks/ 

4. Download the .gitignore, .gitconfig, & .gitattributes files from this into the root of the local repo you just cloned, ie into the folder `<your_repo>/`.

5. Edit .gitconfig with a text editor, replacing `<path to UnityYAMLMerge>` with the location of your Unity install's merge tool (Note that these locations can vary if you picked a different install folder during unity install):
>On Windows it's usually: `C:\\Program Files\\Unity\\Editor\\Data\\Tools\\UnityYAMLMerge.exe` or `C:\\Program Files (x86)\\Unity\\Editor\\Data\\Tools\\UnityYAMLMerge.exe` (double slashes are necessary as escape characters)

>On Mac it's usually: `/Applications/Unity/Unity.app/Contents/Tools/UnityYAMLMerge`

This merge tool will try to merge or resolve conflicts within .prefab, .scene, and other unity asset files. If it can't do it automatically, your default merge tool will open & you can manually select which changes to include. Always open any merged unity assets & confirm the merge worked before pushing the merged assets. For more info, check this: https://github.com/anacat/unity-mergetool or this: http://www.jameskeats.com/blogs/post/Unitys-SmartMerge-Meets-SourceTree/ 

6. Commit these changes to your new repo & push.

## Second: Configure Unity for Git

1. Create a new unity project in the folder you cloned above.

2. Open the editor settings:

`Edit > Project Settings > Editor`

3. Force visible .meta files (this will ensure script execution order & object references are maintained)

`Version Control / Mode: “Visible Meta Files”`

4. Force text serialization (this will ensure you can merge & properly diff your assets)

`Asset Serialization / Mode: “Force Text”`

5. Save changes

`File > Save Project`

## Third: Install GitLFS 

1. Download & install from above link: https://git-lfs.github.com/

2. Open a command prompt, terminal, or gitbash window. 

3. Navigate to the folder containing your git repository & execute: `git lfs install`

4. That's all you need to do, as tracking the appropriate files in lfs is taken care of by the .gitattributes file. If you're already familiar with git, you might consider reading this intro to git-lfs, as working with it varies from vanilla git quite a bit: https://github.com/git-lfs/git-lfs/wiki/Tutorial

## Fourth: Invite everyone else to the repo

1. Make sure they've all installed git lfs!

2. Add them to your repo.
