# Learning to make Discord themes

**<span title="Too long; didn't read">TL;DR</span>: if you don't have the time or energy to read this and just want to set a colour scheme with a background image - use [bdeditor.dev](https://bdeditor.dev/).**

Now for actual content.

This guide assumes that you know how to use your computer, know a little about HTML, and know nothing about CSS or GitHub.

# 1. General CSS
I generally recommend learning the basics of CSS by doing a few hours of not-theme projects or tutorials first. This is because working from a clean slate of nothing is easier than trying to understand what other people have written.

## Cool tutorials
- [Learn CSS in 20 minutes](https://www.youtube.com/watch?v=1PnVor36_40), a youtube video that gives you a speedy overview of CSS.
- [Mozilla's CSS basics](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/CSS_basics), a part of their larger [Get started with the web](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web) tutorial, for those who prefer reading over watching.
- [w3schools' CSS tutorial](https://www.w3schools.com/css/default.asp), a longer guide if you want to go through a more comprehensive guide for the most common uses of CSS.
- [Google's Learn CSS](https://web.dev/learn/css/) - hmmm

Once you have an okay idea of how CSS is structured, you can jump into [Section 2](#2). 

## Useful references

### Properties
- [w3schools](https://www.w3schools.com/cssref/index.php) - simple with some examples for basic usage.
- [mozilla](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference) - slightly more verbose, more precise explanations and comprehensive examples compared to w3schools. 

### Quick references
- [CSS-Tricks' A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/) - `flex` is incredibly useful for aligning stuff, but the property names are many and not particularly descriptive. This explains well what each property does.
- [w3schools' Selector Reference](https://www.w3schools.com/cssref/css_selectors.php) - a list with examples of how to use every selector and selector combinator.

# 2. Custom/Quick CSS and Themes
If you already know some CSS, this is the place to start. I am writing this guide with BetterDiscord in mind, because it is the most accessible client mod for developing themes.

## Get DevTools
DevTools is a requirement to find class names and view Discord's default styles for those classes.

1. Open `Settings` > `BetterDiscord` > `Settings` > `Developer Settings`.
2. Enable the following: 
   - DevTools (mandatory)
   - Debugger Hotkey (convenient for quickly checking hover-only styles)
   - Inspect Element Hotkey (convenient shortcut)
   - Stop DevTools Warning (makes Console tab in devtools actually readable)
3. Open devtools with `Ctrl + Shift + I` (windows/linux) / `Cmd + Opt + I` (mac).

## Writing custom/quick CSS
1. With the Inspect Element tool ![inspect element tool](img/inspectelement.png) (top left corner of devtools), click on some part of Discord that you want to style.
   - Clicking may not always give the exact right element, you may need to go up or down some levels in the document viewer panel.  
![document viewer panel](img/documentviewer.png).
2. Copy the class name and write your styles for it in Custom/Quick CSS. Remember to save (or turn on Live Update) to see your changes.
```css
.content-1gYQeQ {
    border-radius: 8px;
}
```

### Notes about custom CSS:
- In BetterDiscord, Custom CSS is loaded after themes. This means that if a theme and Custom CSS style use the exact same selector and property value, the Custom CSS version will override the theme. 
- In Vencord, this is currently (15th May 2023) the other way round, due to an oversight.
- The in-app editor can be sluggish on less powerful devices, especially with Live CSS enabled. Try an external editor if you experience issues.

## Writing a theme
This is covered by the [BD themes guide](https://docs.betterdiscord.app/themes/introduction/quick-start). Here's a summary:

1. Got to the `themes` folder:
    - Windows: `%appdata%\BetterDiscord\themes`
    - Mac: `~/Library/Application Support/betterdiscord/themes`
    - Linux: `~/.config/BetterDiscord/themes`
2. Make a file with name ending in `.theme.css`:
    - `MyTheme.theme.css`.
3. Start the contents with the theme [meta](https://docs.betterdiscord.app/developers/addons/#meta).
```css
/**
 * @name MyTheme
 * @author MyName
 * @description This is my theme. There are many like it, but this one is mine.
 * @version 1.0
 */
```
4. Finish the contents with your CSS.

### Notes about writing a theme
- The meta is allowed to contain @rules that are not recognised by BetterDiscord, eg. `@license`.

# 3. Publish your theme on github
Sticking your theme on GitHub is a good idea:
1. Convenient for sharing the latest version of the theme with other people.
2. Backup in case the copy on your computer is lost.
3. Can roll back to old versions of the theme if you make a mistake.

## Setting up the repository on Github
1. Make an account.
2. Make a [new repository](https://github.com/new)
    - Set to Public to allow GitHub Pages setup.
    - README, .gitignore, and license can be added later if needed.
3. Click `Add File` and upload your theme file.
3. In the repo's Settings, go to Pages > Build and deployment > Source, selecting `Deploy from a branch`.
4. The option of selecting a branch and folder will now appear. For now, `main` and `/ (root)` are fine. Save the changes.

If you don't intend on making any/many changes to your theme, that's it done. Your theme can now be found at `https://accountname.github.io/reponame/themename.theme.css`.

## Using git(hub desktop) to track your theme updates
1. [Download](https://git-scm.com/downloads) and install git.
2. Install [github desktop](https://desktop.github.com/).
3. Clone your repo: 
    - Github desktop: `File`>`Clone repository...` (or [full guide](https://docs.github.com/en/desktop/contributing-and-collaborating-using-github-desktop/adding-and-cloning-repositories/cloning-and-forking-repositories-from-github-desktop))
    - Command line: `cd "path/to/download/repo/to" && git clone https://github.com/accountname/reponame && cd reponame`
4. Make some changes to your theme inside the folder just created.
5. In GitHub Desktop, select the changed file(s) and write a summary of the changes before clicking `Commit`. This creates a new snapshot of the repository on your computer.
6. To share those changes, click `Push to origin` to push your commit(s) to Github.

There are other more powerful ways of using Git, eg. command line and Git Kraken. For basic purposes though, GitHub Desktop works.

### General advice for git
1. Commit often, so that summaries are easy to write and mistakes can be [reverted](https://stackoverflow.com/questions/4114095/how-do-i-revert-a-git-repository-to-a-previous-commit) without undoing a whole chunk of work.
2. Push (slightly less) often, to avoid data loss if something were to happen to your computer.

## Automatic updates for everyone using your theme
The downside to having all of your styles inside `*.theme.css` is that other people using your theme have to redownload it manually to get updates. 

How do change this? Split the bulk of the CSS into another file, eg. `main.css`, and use `@import` to load it on the fly whenever the `*.theme.css` file is activated.

Since we already set up GitHub Pages while setting up the repository, all that needs to be done is:

1. Create `somefilename.css`.
2. Put your styles into `somefilename.css`.
3. In `*.theme.css*`, immediately following the meta, add the following line (edit as necessary):
   ```css
   @import url("https://accountname.github.io/reponame/somefilename.css");
   ```
4. Commit and push the changes to both files.
5. Wait a few minutes (usually under 2 mins) for GitHub Pages to re-generate.

## Hmm
This is the part where I reccomend scss to solve the problem we just created. but I am too tired to write this so goodnight
