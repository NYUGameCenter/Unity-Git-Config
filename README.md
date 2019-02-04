# Unity-Git-Config
Here is where we maintain exemplar git configuration files for Unity3d projects

Setup instructions:

# First
Create a repo on github

Clone the repo to your local machine.

Download the .gitignore & .gitattributes files from this into the local repo you just cloned.

Add these two files as the first commit to your new repo.

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
