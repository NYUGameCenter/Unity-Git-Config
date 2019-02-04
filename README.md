# Unity-Git-Config
Here is where we maintain exemplar git configuration files for Unity3d projects

Setup instructions:

# First
Create a repo on github & configure it

Clone the repo to your local machine.

Download the .gitignore, .gitconfig, & .gitattributes files from this into the local repo you just cloned.

Edit .gitconfig with a text editor, replacing '<path to UnityYAMLMerge>' with the location of your Unity install's merge tool: 
On Windows it's usually: C:\Program Files\Unity\Editor\Data\Tools\UnityYAMLMerge.exe or C:\Program Files (x86)\Unity\Editor\Data\Tools\UnityYAMLMerge.exe
On Mac it's usually:
/Applications/Unity/Unity.app/Contents/Tools/UnityYAMLMerge

Note that these locations can vary if you picked a different install folder during unity install.

After editing the .gitconfig, add it, & the the rest these files, as the first commit to your new repo.

# Second
Properly configure Unity for git

Open the editor settings:
Edit > Project Settings > Editor

Force visible .meta files (this will ensure script execution order & object references are maintained)
Version Control / Mode: “Visible Meta Files”

Force text serialization (this will ensure you can merge & properly diff your assets)
Asset Serialization / Mode: “Force Text”

Save changes
File > Save Project

# Third
Install & configure gitlfs: https://git-lfs.github.com/

Download & install from above link

Open a command prompt, terminal, or gitbash window. 

Navigate to the folder containint your git repository & run: git lfs install

# That's it!
