# Description

This folder contains a shareable Vue.js component library used across multiple projects (e.g., Portal, Website). It includes reusable UI components, styles, and utility functions to maintain design and code consistency across applications.

## Features

- Vue 2 compatible
- Easy integration via Git submodules
- Update at project or global level

# Commands

Add the submodule to a folder

```
git submodule add <repo-url> path/to/submodule-folder
git submodule add git@github.com:NevetsKuro/vue-library.git src/vue-library
```

Cloning the repo

```
git clone --recurse-submodules <repo-url>
git clone --recurse-submodules git@github.com:NevetsKuro/vue-library.git
```

Updating Submodules

```
Way #1
git submodule update --remote
git submodule update --remote --merge
```

```
Way #2
cd path/to/submodule
git checkout main  # or master
git pull origin main
cd ..
git add path/to/submodule
git commit -m "Update submodule"
```

Removing Submodules

```
git rm --cached path/to/submodule
rm -rf path/to/submodule
```

Incase, vue-library folder is indexed
`git rm --cached -r src/vue-library`
