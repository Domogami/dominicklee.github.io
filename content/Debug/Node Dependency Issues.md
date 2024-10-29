---
title: Node Dependency Issues
---

## Basic Remedy

If you are ever having strange node dependency issues, this is what helped me

````shell
rm -rf node_modules
rm package-lock.json yarn.lock
npm cache clear --force
npm install
````

## Node Version Manager

I often have issues related to multiple projects using multiple versions of node. To make switching between Node Version 14 to Node Version 18 and then to 21, I use [NVM (Node Version Manager)](https://github.com/nvm-sh/nvm) to quickly switch my version of Node.js

````shell
nvm use 21
````
