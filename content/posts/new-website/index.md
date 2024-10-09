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
  - Search for `dateFormat` in the repo, find example, and copy `dateFormat = "January 2, 2006"` into params section of config file.
  - Site builds locally...now to try on cloudflare!
  - Actually get issue I had before but did not write. There is some delay in cloudflare looking at the latest commit. It is still using old commit.
  - Aaaand it turns out I actually forgot to push the changes... Doh! There is still some kind of delay though.
  - It works!
  - When I click on blogpost though, it goes to `example.org/posts/new-website` so need to update that.
  - Find https://developers.cloudflare.com/pages/how-to/custom-branch-aliases/
  - This doc is for getting access other other branches of my github repo, but importantly it points me to the 'Custom domains' tab. I try adding `www.lovkush.com`. Says it might take 48 hours to update.
  - And now I go to Claude to try to understand all this. This does help me get some sense of what is going on, e.g. how when somebody enters `www.lovkush.com` somehow request goes to hover, then to cloudflare, and then via DNS settings in cloudflare to the deployed page hosted on cloudflare. Also explaining how `www` is not actually necessary and is just an old convention that has stuck around!
  - After fiddlig with DNS settings in cloudflare, now when I go to www.lovkush.com I no longer get my old website, and instead get error message. Seems it is because I added a `/` at the end of the url provided in the 'content' entry in dns management table. Now get error 'Connection time out'. Maybe it is something about timing. Wait a bit and try again - it goes to original website! Hmm...this is confusing.
  - Ask Claude for suggestions. Try purging cache and using incognito browser and still goes to original website. Claude also suggested just need to wait for DNS changes to propagate throughout the system. Hmm.
  - After playing around, looks like difference is using http vs https. With secure one it goes to new website but not with http. So need to find rule on cloudflare for this!
  - Spend maybe hour now, with Claude giving detailed instructions, trying to debug. Do not make any progress so take break.
  - Come back and try to undo changes Claude suggested (around always using https). Now it seems to work using `lovkush.com` while `www.lovkush.com` points to my old website.
  - Next, update the base url, because it was still using default of example.org.

