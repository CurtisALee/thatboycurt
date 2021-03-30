# The site

The main build and configuration for this site was bootstrapped from the old [Leaf website][leaf], prior to the Docker integration. I've simply taken the foundation of the original codebase, hooked it up Netlify, and stripped the files back in order to add my own content and sprinkle of CSS.

[leaf]: https://weareleaf.com/

My initial set-up for this was slightly different to the original Leaf docs (which I'll include below), so I'm referencing them here for my own (and future Curt's) sake incase I run into the same issues again.

## Installing nvm

This project uses node `10.20.1` (Found in the `.nvmrc` file). In order to flick between different node versions on your system, you need to [install nvm][nvm].

[nvm]: https://github.com/nvm-sh/nvm

Once you've ran the install script, you can then run `nvm install 10.20.1` to grab the required version of node, and then `nvm use 10.20.1` if you have another version of node already installed (Can omit this step if you don't).

In an ideal world, this will work. If, however, you're setting up a new Mac like I was, you can follow the steps below to avoid losing an hour of your Sunday morning.

## Fix for nvm: command not found

By default, MacOS uses `zsh` as the shell. Despite this, the required `.zshrc` file isn't created by default on a new Mac, which means that when you install `nvm`, it doesn't add the necessary scripts to the file... Because it doesn't exist (Ugh).

To resolve this:

run `touch ~/.zshrc` to create the file in your root folder
then run `nano ~/.zshrc` to open the file in the terminal
then paste in this script: `export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")" [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm`
press `ctrl + X` to exit the editor
press `Y` to save
press `Enter` to return to folder

Once you've done this, check to make sure `nvm` is installed using `command -v nvm`. If it returns `nvm $`, the fix worked! You should now be able to run `nvm install 10.20.1` again to get the required node version. If it doesn't work, simply close the laptop lid and forget about it 👍🏻

---

# Deploying to Netlify

This repository is synced to Netlify, and every time new changes are pushed, Netlify automatically runs the build and deploys the site live to [thatboycurt.com][site].

The build command and DNS settings are stored in the `Site Overview` on Netlify, so unless they're changed, there's nothing more that needs to be done...

[site]: https://thatboycurt.com/

The original documenation from the Leaf site is below, which also includes the standard `npm install` step as well 💙:

---

# Leaf Website

This is Leaf's static site build. It uses [Pug](https://pugjs.org/api/getting-started.html) for the templating, [npm](https://www.npmjs.com/) for client side dependencies, [Sass](https://sass-lang.com/) for styling and [Webpack](https://webpack.js.org) for the build.

## Initial Setup

First, install [Homebrew](https://brew.sh) and use it to set up [NVM](https://github.com/creationix/nvm) (Node Version Manager):

```
brew install nvm
```

Then, install the required version of node and install the dependencies for the project:

```
nvm install 10.20.1
nvm use
npm install
```

## Usage

- Run `npm run start` run the development server
- Run `npm run build:jpgs` to create jpg copies of all png images on the site with a `#3d18c3` background colour.
- Run `npm run deploy` to build a production ready version of the site and deploy it to https://weareleaf.com

## Development Notes

- Once started, the development server should be viewable at http://localhost:3000.
- Changes to Pug and JavaScript files should automatically reload the page.
- Changes to SCSS will not automatically reload the page.
- When you add new files, you'll need to restart the development server for them to be picked up.
- If you want to change the background colour of generated jpg images, update the value in `scripts/png-convert.js`.

## Adding blog posts

1.  Copy the existing blog post `src/pages/blog/goals-matter` to a new file. Choose a sensible name with dash-separated words, as this will form the URL of your post.
2.  Start or restart the development server so that it picks up the new file.
3.  View your post at http://localhost:3000/blog/your-post-filename
4.  Edit your blog content by updating your new pug file.
5.  Update the variables at the top of your blog post file, this is important as they're used to display a correct link preview when sharing on social media.
6.  Update the `gridItems` array in `src/assets/scripts/blog.js` to include an entry for your blog post as the the first entry in the array. This will ensure the blog post displays on http://localhost:3000/blog, and is included in the thumbnails at the bottom of each blog post automatically.
7.  Check everything is as you want it, and put your post up for review by submitting a pull request on Github!

Enjoy ❤️
