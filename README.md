# Unity-Git-Config
Here is where we maintain exemplar git configuration files for Unity3d projects

# Setup instructions:

## First: Create & Configure Your Repo 

1. Create a new github repo.

2. Clone the repo to your local machine.

3. Download the .gitignore, .gitconfig, & .gitattributes files from this into the local repo you just cloned.

4. Edit .gitconfig with a text editor, replacing `<path to UnityYAMLMerge>` with the location of your Unity install's merge tool: 
On Windows it's usually: `C:\Program Files\Unity\Editor\Data\Tools\UnityYAMLMerge.exe` or `C:\Program Files (x86)\Unity\Editor\Data\Tools\UnityYAMLMerge.exe`
On Mac it's usually: `/Applications/Unity/Unity.app/Contents/Tools/UnityYAMLMerge`
Note that these locations can vary if you picked a different install folder during unity install.

5. After editing the .gitconfig, add it, & the the rest these files, as the first commit to your new repo.

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
