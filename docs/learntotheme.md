# Learn To Theme

**<span title="Too long; didn't read">TL;DR</span>: Use [bdeditor.dev](https://bdeditor.dev/), if you just want to set a colour scheme with a background image, and don't have the time or energy to read this page.**

*Now for actual content.*

This guide assumes that you know:
- how to use your computer,
- a little about HTML, and
- nothing about CSS or GitHub.

I am writing this guide with [BetterDiscord](https://betterdiscord.app/) in mind, because it is the most accessible client mod for developing themes. However, the general principles apply to most desktop client mods, for example [Replugged](https://replugged.dev/) and [Vencord](https://GitHub.com/Vendicated/Vencord).

## Step 1: Learning general CSS
Learning the basics of CSS by doing a few hours of not-theme projects or tutorials first. This is because working from a clean slate of nothing is easier than trying to understand what other people have written. Once you have a decent grasp of what CSS is and how you could use it. you can head over to Step 2.

### Tutorials
| Link                                                                                                             | Description                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [Web Dev Simplified's *Learn CSS in 20 minutes*](https://www.youtube.com/watch?v=1PnVor36_40)                    | A video that gives you a speedy overview of CSS.                                                                                                                                                             |
| [Mozilla's *CSS Basics*](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/CSS_basics) | A document similar to the video above, being a quick overview of CSS. Part of an overall [*Get started with the web*](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web) tutorial. |
| [w3schools' *CSS Tutorial*](https://www.w3schools.com/css/default.asp)                                           | A longer practical-first guide. Includes exercises and quizzes.                                                                                                                                              |
| [Google's *Learn CSS*](https://web.dev/learn/css/)                                                               | A longer theory-first guide. Includes exercises and quizzes.                                                                                                                                                 |

### Useful reference material

#### Properties
| Link                                                                  | Description                                                                                        |
| --------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| [w3schools](https://www.w3schools.com/cssref/index.php)               | Simple with some examples for basic usage.                                                         |
| [Mozilla](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference) | Slightly more verbose, more precise explanations and comprehensive examples compared to w3schools. |

#### Other

| Link                                                                                                              | Description                                                                                                                                                                                              |
| ----------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [CSS-Tricks' *A Complete Guide to Flexbox*](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)              | `flex` is incredibly useful for arranging content in a container without hardcoding sizes, but the property names are many and not particularly descriptive. This explains well what each property does. |
| [CSS-Tricks' *A Complete Guide to CSS Grid*](https://css-tricks.com/snippets/css/complete-guide-grid/)            | `grid` is the modern way to tile content, and this again helps with the terminology.                                                                                                                     |
| [w3schools' *CSS Selector Reference*](https://www.w3schools.com/cssref/css_selectors.php)                         | A list with examples of how to use every selector and selector combinator.                                                                                                                               |
| [Chrome Developers' *DevTools CSS features reference*](https://developer.chrome.com/docs/devtools/css/reference/) | A guide for using DevTools effectively in Chrome/Chromium.                                                                                                                                               |

## Step 2: Writing Custom CSS and Themes
If you know some CSS, this is the place to start.

### Developer settings
Before beginning DevTools is a requirement to find class names and view Discord's default styles for those classes.

1. Open `Settings` > `BetterDiscord` > `Settings` > `Developer Settings`.
2. Enable the following: 
   - DevTools (mandatory)
   - Debugger Hotkey (convenient for quickly checking hover-only styles)
   - Inspect Element Hotkey (convenient shortcut)
   - Stop DevTools Warning (makes Console tab in devtools actually readable)
3. Open DevTools with `Ctrl + Shift + I` (windows/linux) / `Cmd + Opt + I` (mac).

### Writing Custom CSS
1. With the ![inspect element tool](img/inspectelement.png) Inspect Element tool (top left corner of devtools), click on an area that you want to style.
   - Clicking may not always give the exact right element, you may need to go up or down some levels in the document viewer panel.  
![document viewer panel](img/documentviewer.png).
2. Copy the class name and write your styles for it in Custom CSS. Remember to save (and/or turn on Live Update) to see your changes.  
```css
.content-1gYQeQ {
    border-radius: 8px;
}
```

#### Notes
- In BetterDiscord, Custom CSS is loaded after themes. This means that if a theme and Custom CSS style use the exact same selector and property value, the Custom CSS version will override the theme. In Vencord's QuickCSS, this is currently (15th May 2023) the other way round, due to an oversight.
- The in-app editor can be sluggish on less powerful devices, especially with Live CSS enabled. Try an external editor if you experience issues.

### Writing a theme
This is covered by the [BD themes guide](https://docs.betterdiscord.app/themes/introduction/quick-start). Here's a summary:

1. Go to the `themes` folder:
    - Windows: `%appdata%\BetterDiscord\themes`
    - Mac: `~/Library/Application Support/betterdiscord/themes`
    - Linux: `~/.config/BetterDiscord/themes`
2. Make a file with name ending in `.theme.css`, eg. `MyTheme.theme.css`.
3. Start the contents with the theme [meta](https://docs.betterdiscord.app/developers/addons/#meta), eg.
```css
/**
 * @name MyTheme
 * @author MyName
 * @description This is my theme. There are many like it, but this one is mine.
 * @version 1.0
 */
```
4. Add your CSS rules after the meta.

#### Notes
- The meta is allowed to contain other fields that are not recognised by BetterDiscord, eg. `@license`.

## Step 3: Using Git and GitHub to track changes
Using Git to track changes, and uploading the theme to GitHub, provide several benefits:
1. Convenience for sharing the latest version of the theme with other people.
2. Backup in case the copy on your computer is lost.
3. Ability to roll back to old versions of the theme if you make a mistake.
4. If your theme meets the [BetterDiscord theme guidelines](https://docs.betterdiscord.app/themes/introduction/guidelines), you can then [submit the theme](https://docs.betterdiscord.app/developers/submitting/)'s GitHub repository for review to potentially become an official theme.

### Setting up the theme repository on GitHub
1. [Make a GitHub account](https://github.com/signup).
2. Make a [new repository](https://GitHub.com/new).
    - Set visibility to Public, to allow setting up GitHub Pages.
    - README, .gitignore, and license can be added later if needed.
3. Click `Add File` and upload your theme file.
4. In the repository's Settings, go to `Pages` > `Build and deployment` > `Source`, selecting `Deploy from a branch`.
5. The option of selecting a branch and folder will now appear. For now, `main` and `/ (root)` are fine. Save the changes.

If you don't intend on making many/any changes to your theme, that's it done. Your theme can now be found at `https://accountname.github.io/reponame/themename.theme.css`. eg. https://saltssaumure.github.io/xp-discord-theme/Exponent.theme.css

### Using Git to track your theme updates
1. [Download](https://git-scm.com/downloads) and install Git.
2. Install [GitHub Desktop](https://desktop.GitHub.com/).
3. [Clone your repository](https://docs.github.com/en/desktop/contributing-and-collaborating-using-github-desktop/adding-and-cloning-repositories/cloning-and-forking-repositories-from-github-desktop) (ie, download it to your computer).
4. Inside the folder just created (which will be your repository's name by default), make any changes you like to the contents. You could edit the theme file, add other files, or delete unwanted files. Just don't change the `.git` folder or its contents.
5. Create a commit, a snapshot of the current state of the repository. In GitHub Desktop, [select the changed file(s)](https://docs.github.com/en/desktop/contributing-and-collaborating-using-github-desktop/making-changes-in-a-branch/committing-and-reviewing-changes-to-your-project-in-github-desktop#selecting-changes-to-include-in-a-commit) and [write a summary of the changes](https://docs.github.com/en/desktop/contributing-and-collaborating-using-github-desktop/making-changes-in-a-branch/committing-and-reviewing-changes-to-your-project-in-github-desktop#write-a-commit-message-and-push-your-changes) before clicking `Commit`.
    - Commit often, so that summaries are easy to write and mistakes can be [reverted](https://stackoverflow.com/questions/4114095/how-do-i-revert-a-git-repository-to-a-previous-commit) without undoing a larger amount of work.
6. Push your commit(s) to GitHub to sync your changes, by clicking `Push to origin`.

There are other more powerful ways of using Git, eg. command line and GitKraken. For basic purposes though, GitHub Desktop works just fine.

## Step 4: Set up automatic theme updating
Having your whole theme in a single `*.theme.css` file is a quick and convenient way to start writing a theme, but comes with two main downsides.

- The file can get excessively long and hard to navigate.
- People using your theme have to manually redownload to get updates.

To solve both of these issues, we can instead split the bulk of the CSS into another file, eg. `main.css`, and use `@import` to load it on the fly whenever the `*.theme.css` file is activated.

1. Create your subfile, for example `innerworkings.css`.
2. Put your styles into `innerworkings.css`.
3. In `*.theme.css*`, immediately following the meta, add the following line, replacing the exact features as required:
   ```css
   @import url("https://accountname.github.io/reponame/innerworkings.css");
   ```
4. Commit and push the changes to both files.
5. Wait a few minutes (usually under 2 mins) for GitHub Pages to re-generate.

Now, by simply toggling the theme in the Settings > Themes, the newest version of `innerworkings.css` is loaded without needing to redownload the `*.theme.css` file.

## Step 5: Theme development tools
Now that the theme's main contents are stored in a separate CSS file that is downloaded on the fly, we encounter a new problem. Changes to `innerworkings.css` can only be seen after being uploaded and processed by GitHub, rather than loading from your own computer. Obviously this would be a tedious way to develop.


1. Install Gibbu's [create-bd-theme](https://github.com/Gibbu/create-bd-theme) tool 
