# The site

The main build and configuration for this site was bootstrapped from the old [Leaf website][leaf], prior to the Docker integration. I've simply taken the foundation of the original codebase, hooked it up Netlify, and stripped the files back in order to add my own components and sprinkle of CSS.

[leaf]: https://weareleaf.com/

My initial set-up for this was slightly different to the original Leaf docs, so I'm referencing them here for my own (and future Curt's) sake incase I run into any issues in the future.

## Installing nvm

This project uses node `10.20.1` (Found in the `.nvmrc` file). In order to flick between different node versions on your system, you need to [install nvm][nvm].

[nvm]: https://github.com/nvm-sh/nvm

Once you've ran the install script, you can then run `nvm install 10.20.1` to grab the required version of node, and then `nvm use 10.20.1` if you have another version of node already installed (Can omit this last step if you don't).

In an ideal world, this will work. If, however, you're setting up a new Mac like I was, you can follow the steps below to avoid losing an hour of your Sunday morning.

## Fix for nvm: command not found

By default, MacOS uses `zsh` as the shell. Despite this, the required `.zshrc` file isn't created by default on a new Mac, which means that when you install `nvm`, it doesn't add the necessary scripts to the file to make it work... because it doesn't exist (Ugh).

To resolve this:

- run `touch ~/.zshrc` to create the file in your root directory
- then run `nano ~/.zshrc` to open the file in the terminal
- then paste in this script: `export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")" [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm`
- press `ctrl + X` to exit the editor mode
- press `Y` to save
- then press `Enter` to return to the root folder

Once you've done this, check to make sure `nvm` is installed using `command -v nvm`. If it returns `nvm $`, the fix worked! You should now be able to run `nvm install 10.20.1` again to get the required node version. If it doesn't work, simply close the laptop lid and forget about it 👍🏻

## Installing the node modules

This bits easy -> `cd/into/thatboycurt`, and run `npm install` to create the `node_modules` folder. This will install all of the required dependencies for the project, and once this is done, use `npm start` to launch the local server. All changes will be automatically compiled and refreshed in the browser from here on out.

---

# Deploying to Netlify

This repository is synced to Netlify, and every time new changes are pushed, Netlify automatically runs the build and deploys the site live to [thatboycurt.com][site].

I've set the build command and DNS settings in the `Site Overview` section on Netlify, so unless they're changed, there's nothing more that needs to be done...

[site]: https://thatboycurt.com/

---

Again, a big thanks to the Leaf team for supplying the config for this 💙
