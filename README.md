# Branchline

A planning network. Tasks are stations on transit lines, track length is time, and a split-flap departure board sorts everything by day. Everything is edited with the mouse.

Sign on with operator ID `t205` and key `spl`.

## How your data is saved

- **This browser:** every change is saved instantly and survives closing the tab or restarting the computer.
- **GitHub (once linked):** about 2.5 seconds after your last edit, the network is committed to `data/network.json` in a private repo. Open the site on another device, link it with a token, and it loads the same network. Changes made elsewhere are pulled in when you come back to the tab.

## Setup (about 5 minutes)

You need two repos. The site repo must be public for free GitHub Pages. A public repo would also make your tasks public, so the data lives in a separate private repo.

1. **Site repo.** Create a public repo named `branchline`. Upload `index.html`, `.nojekyll`, and this README to the root of `main`.
2. **Turn on Pages.** In the site repo, go to Settings, then Pages. Under Build and deployment, choose "Deploy from a branch", branch `main`, folder `/ (root)`, and save. After a minute or two the site is live at `https://YOUR-USERNAME.github.io/branchline/`.
3. **Data repo.** Create a **private** repo named `branchline-data`, with "Add a README file" checked so it has a `main` branch. Leave it otherwise empty. Branchline creates `data/network.json` itself on the first save.
4. **Access token.** Go to GitHub Settings, then Developer settings, then Personal access tokens, then Fine-grained tokens, then Generate new token. Fill it in like this:
   - Name: `branchline`
   - Expiration: whatever you're comfortable with, e.g. 1 year
   - Repository access: **Only select repositories**, with `branchline-data` selected
   - Permissions: under Repository permissions, set **Contents** to **Read and write** (Metadata read-only is added automatically)

   Generate it and copy the token. It starts with `github_pat_`.
5. **Link it.** Open the site and sign on. With no stop selected, find the **Data link** plate in the right column (or click the Data link tile in the header). The data repo is pre-filled as `YOUR-USERNAME/branchline-data`. Paste the token and press **Link to GitHub**. The Data link tile turns green.

Repeat step 5 on each device you use. The token is stored only in that browser and is never written into the site or the repo.

## Prompt for Claude in Chrome

Paste this into Claude in Chrome with the three files ready to upload. It stops before the token so you can copy that yourself:

> Help me set up GitHub for my Branchline site. I'm signed in to GitHub. Please:
> 1. Create a new **public** repository named `branchline` and upload the files `index.html`, `.nojekyll` and `README.md` I give you to the root of `main`.
> 2. In that repo's Settings > Pages, set the source to "Deploy from a branch", branch `main`, folder `/ (root)`, and save. Tell me the site URL.
> 3. Create a new **private** repository named `branchline-data` with "Add a README file" checked.
> 4. Open Settings > Developer settings > Personal access tokens > Fine-grained tokens > Generate new token. Name it `branchline`, set Repository access to "Only select repositories" with just `branchline-data`, and set Repository permissions > Contents to "Read and write". Stop on the page before generating so I can review it and generate it myself.

## Honest limits

- **The sign-on is a front-door lock, not security.** A static site can't keep a secret: a hash of the ID and key sits in the page source, and a three-letter key can be guessed by anyone who tries. It keeps casual visitors out. Your data is actually protected by the private repo and the token.
- **One save, one commit.** Each save is a commit to `branchline-data`. Saves wait until you pause editing, but a busy session can still produce dozens of commits. That's harmless, and it also gives you a full history to roll back to.
- **Two devices editing at once means the last save wins.** Branchline pulls newer changes when you return to a tab, but it doesn't merge edits made at the same moment on two devices.
- **The Claude preview can't reach GitHub.** In the preview copy of Branchline, the Data link will report an error. Sync only works on your GitHub Pages site.
