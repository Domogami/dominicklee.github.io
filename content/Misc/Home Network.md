---
title: Automating Obsidian Publish
---

## Script

To make it easier for me to keep my website up to date with my personal vault, I needed to automate the publish process. Below is a script I can trigger from RayCast in order to quickly update my website with a simple trig\[[]()\]()ger and confirmation key.

````bash
#!/bin/bash

# Remove Old Files
trash /Users/dom/Documents/GitHub/obsidian-site/quartz/content/*
trash /Users/dom/Documents/GitHub/obsidian-site/quartz/public/*

# Export my Obsidian Vault to the GitHub content folder
/Users/dom/Documents/GitHub/obsidian-site/obsidian-export/target/debug/obsidian-export --frontmatter=always ~/Library/Mobile\ Documents/iCloud~md~obsidian/Documents/Dom\'s\ 2nd\ Brain/ /Users/dom/Documents/GitHub/obsidian-site/quartz/content

# Compile Quartz Site
cd /Users/dom/Documents/GitHub/obsidian-site/quartz
npx quartz build

# Save today's date for the commit name
date=$(date '+%m-%d-%Y')

# Output current changed files
OUTPUT="$(git status)"
echo "${OUTPUT}"

# A helper function to ask for confirmation
asksure() {
	echo -n "Are you sure (Y/N)? "
	while read -r -n 1 -s answer; do
	  if [[ $answer = [YyNn] ]]; then
	    [[ $answer = [Yy] ]] && retval=0
	    [[ $answer = [Nn] ]] && retval=1
	    break
	  fi
	done
	
	echo # just a final linefeed, optics...
	
	return $retval
}

if asksure; then
	# Publish!
	git add .
	git commit -m "✨ [FEAT] $date Update"
	git push
	
	echo "Published! 🚀"
else
	echo "Aborting! ❌"
fi
````
