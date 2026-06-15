### Local Git's Workflow

1. Working Directory 
2. Stage -> Changes are ready to save
3. Local Repository -> A place where all the versions of the files and thier complete change history is stored by system files that are managed entirely by Git
---
##### Working Directory -> Stage [Stage]

- To Review, Adjust or Remove Changes

`git add --all (or) -A`
-> Stage all changes to be committed

`git add .`
->Stage only changes in the current directory and every thing inside it

`git add *`
->Only stages new or modified files but **NOT DELETED ONES**

`git add file.xx (or) folder/`file.xx
-> Stage specific files

`git add *.extension`
-> Stages all files with the specified extension

`git reset`
->  Unstage changes

---
##### Stage -> Local Repository [Commit]

- To make the staged changes permenant
  
  `git commit -m "I have made some changes to files`
  -> To commit files and (`-m`) is to leave a short message


	