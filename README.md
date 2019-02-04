# Unity-Git-Config
We've put together some git configuration files to cover the majority of Unity/Git use cases & identify as many large file types as possible prevent your repos from filling up with cruft. 

# Setup instructions:

## First: Create & Configure Your Repo 

1. Create a new github repo.

2. Clone the repo to your local machine.

3. Download the .gitignore, .gitconfig, & .gitattributes files from this into the local repo you just cloned.

4. Edit .gitconfig with a text editor, replacing `<path to UnityYAMLMerge>` with the location of your Unity install's merge tool: 
On Windows it's usually: `C:\\Program Files\\Unity\\Editor\\Data\\Tools\\UnityYAMLMerge.exe` or `C:\\Program Files (x86)\\Unity\\Editor\\Data\\Tools\\UnityYAMLMerge.exe` (double slashes are necessary as escape characters)
On Mac it's usually: `/Applications/Unity/Unity.app/Contents/Tools/UnityYAMLMerge`
Note that these locations can vary if you picked a different install folder during unity install. This merge tool will try to merge or resolve conflicts within .prefab, .scene, and other unity asset files. If it can't do it automatically, your default merge tool will open & you can manually select which changes to include. Always open any merged unity assets & confirm the merge worked before pushing the merged assets. For more info, check this out: https://github.com/anacat/unity-mergetool

5. After editing the .gitconfig, add it & the the rest these files, as the first commit to your new repo.

## Second: Configure Unity for Git

1. Open the editor settings:

`Edit > Project Settings > Editor`

2. Force visible .meta files (this will ensure script execution order & object references are maintained)

`Version Control / Mode: “Visible Meta Files”`

3. Force text serialization (this will ensure you can merge & properly diff your assets)

`Asset Serialization / Mode: “Force Text”`

4. Save changes

`File > Save Project`

## Third: Install GitLFS 

1. Download & install from above link: https://git-lfs.github.com/

2. Open a command prompt, terminal, or gitbash window. 

3. Navigate to the folder containing your git repository & execute: `git lfs install`

# That's it!
