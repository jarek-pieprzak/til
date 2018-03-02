# React GitHub Pages #

**1. Add `homepage` to `package.json`**

Open `package.json` and add a `homepage`field for your project: 

```
"homepage": "https://username.github.io/my-app",
```
or for GitHub user (main) page:
```
"homepage": "https://username.github.io",
```

**2. Install `gh-pages` and `deploy` to `scripts` in `package.json`**

Now, run `npm run build`.

To publish it at GitHub Pages, run: 
`yarn add gh-pages`

Add the following to package.json: 

`"predeploy": "npm run build",`

`"deploy": "gh-pages (optional branch for build)-d build",`

**3. Deploy the site by running `npm run deploy`**


# **and that's it!**
