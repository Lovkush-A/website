---
date: 2024-10-09
# description: ""
# image: ""
lastmod: 2024-10-09
showTableOfContents: false
# tags: ["",]
title: "New Website"
type: "post"
---

This post explains the steps I took to create this new website.

Resources used:
- https://swe-to-mle.pages.dev/posts/learn-in-public/
- https://gokarna-hugo.netlify.app/posts/theme-documentation-basics

Steps
- Set up hugo and the theme
  - `brew install hugo`
  - `hugo new site website`
  - `git submodule add https://github.com/526avijitgupta/gokarna.git themes/gokarna`
  - Copy the example config file from gokarna docs into `hugo.toml`

- Create blogpost
  - `hugo new posts/new-website/index.md`.
  - Then write this blogpost! This is done in parallel with the remaining steps.

- Test locally
  - `hugo serve`
  - `open http://localhost:1313`

- Push to GitHub

- Set up cloudflare
  - [https://pages.cloudflare.com/](https://pages.cloudflare.com/)
  - Create account
  - Feel overwhelmed with the dashboard...eep!
  - Find this which seems promising. `https://developers.cloudflare.com/pages/get-started/git-integration/`
  - Go back to dashboard and go to homepage. Now giving me instructions about adding new domain!
  - So I enter `lovkush.com` and it provides some instructions.
  - Then need to log in to my domain registrar. I use hover.
  - Something about avoiding DNS. Click around in hover and looks like I dont need to do anything...
  - Update nameservers
  - Cloudflare says it can take 24 hours for things to be updated... This is not the kind of feedback cycle I am hoping for! Especially when I have no understanding. If things do not work, I have no intuition for which step I should check first.
  - Now back to the git integration. Click on workers & pages in left hand menu.
  - Contrary to docs, I click on the 'Pages' tab and then option to 'Connect to Git' appears.
  - Give access to my repo
  - Click 'Begin setup'
  - Change project name, it says project will be deployed on `personal-website-epg.pages.dev`
  - Select Hugo from Framework preset. Assume the other things are correct - I think it matches what I saw from the docs for gokarna.
  - Click 'Save and deploy'.
  - Get bug... `Unable to locate config file or config directory`
  - The blogpost at the top did use `config.toml` instead of `hugo.toml`, so just try renaming.
  - Now get different error. Progress! `Error building site...<.Site.Params.dateFormat>: invalid value; expected string`
  - I get the same error locally too.
  - Search for `dataFormat` in the repo, find example, and copy `dateFormat = "January 2, 2006"` into params section of config file.
  - Site builds locally...now to try on cloudflare!
  


