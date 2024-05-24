---
title: "Gitexercises"
date: 2024-05-24T08:00:35+05:30
draft: false
---

# Git Exercises

## 1. Push a commit you have made

This one was straightforward and easy, command(s) used : 

```
git verify
```

## 2. Commit one file 

This just involved adding the individual file and then commiting it.

```
git add A.txt
git commit -m "Commit A.txt file"
```

## 3. Commit one file of two currently staged

I reseted the staged files, added the one i wanted and commited it.

```
git reset
git add "A.txt"
git commit -m "A.txt"
```

## 4. Ignore unwanted files

I added the unwanted files and directories into the .gitignore file

```
touch .gitignore
vim .gitignore
git add .gitignore
git commit -m "added gitignore file"
```

## 5. Chase branch that escaped

I merged the 'escaped' branch into 'chase-branch'

```
git merge escaped
```

## 6. Resolve a merge conflict

I edited the 'equation.txt' file in vim to contain '2 + 3 = 5'

```
git merge another-piece-of-work
vim equation.txt
git add equation.txt
git commit -m "."
```

## 7. Saving your work

At first I got it wrong, then hint came up referig to that, I stashed the existing changes, made the required changes, poped te stash and commited.

```
git stash
git commit -m "bug"
git stash pop
git add --all
vim bug.txt
git commit -m "done"
```

## 8. Change branch history

Okay, now this one required a tiny bit of googling to know about the rebase command.

```
git rebase hot-bugfix
```

## 9. Remove ignored file

This one was fairly easy.

```
git rm ignored.txt
git commit -m "ignored"
```

## 10. Change a letter case in the filename of an already tracked file

This was straightforward.

```
git mv File.txt file.txt
git add --all
git commit -am "file name change"
```

## 11. Fix typographic mistake in the last commit

This was my first time using 'amend' command and it took a fair bit of googling.

```
vim file.txt
git add --all
git commit --amend
```

## 12. Forge the commit's date

I have tried this one before just out of curiosity, it was quick

```
git commit --date="1987-01-01 12:12:00" --amend
```

## 13. Fix typographic mistake in old commit

This needed some googling to get done

```
git rebase -i HEAD^^
git add --all
git rebase --continue
```

## 14. Find a commit that has been lost

I got this wrong a couple of times then the hint came up, that helped.

```
git reflog
git reset HEAD~
```

## 15. Split the last commit

This was fairly easy given i learned about reset in last exercise

```
git reset HEAD~
git add first.txt
git commit -m "first"
git add second.txt
git commit -m "second"
```

## 16. Too many commits

This was fairly easy, I rebased HEAD, then add all and commit

```
git rebase -i HEAD~2
git add --all
git commit -m '."
```

## 17. Make the file executable by default

I got it to work after some googling

```
git update-index --add --chmod=+x script.sh
```

## 18. Commit part of work

First I didnt get how to search and select the needed lines inside the file, took me quite a bit of time to figure it out

```
git add -p file.txt
git commit -m "first"
git add --all
git commit -m "second"
```

## 19. Pick your features

I condnt get the right command for the first few times, after some time i came across cherry-pick and that got it done

```
git cherry-pick feature-a
git cherry-pick feature-b
git cherry-pick feature-c
git add --all
git rebase --continue
```

## 20. Rebase complex

I did the using rebase --onto after reading it in git docs

```
git rebase issue-555 --onto your-master
```

## 21. Change order of commits

This was easy, but took a couple tries as I ordered it wrong

```
git rebase -i HEAD~2
```

## 22. Find commits that introduced swearwords

This one took multiple tries too because of minor mistakes

```
git log -S shit
git rebase -i e97ac9901697708a57a1bc266b5b7b173024fc05f^
vim list.txt
vim words.txt
git add --all
git commit --amend
git rebase --continue
```

## 23. Find commit that has introduced bug

This exercise took a lot of time as I kept getting error, turns out openssl was not installed. After I installed openssl, did bisect good and bad to finally find the correct one

```
git bisect start
git bisect bad
git bisect good 1.0
git bisect run sh -c "openssl enc -base64 -A -d < home-screen-text.txt | grep -v jackass"
git push origin 4663d3b4f09e624ed13af8bb5e25f6d4a8bd1304:find-bug
```