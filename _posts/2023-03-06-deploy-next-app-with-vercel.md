---
title: Deploying a Next.js app with Vercel
categories: [DevOps]
layout: post
excerpt: "Last week I deployed a Next.js app to Vercel. It was one of the easiest deployments I've done."
---

Hola. 👋🏾

Last week I deployed a Next.js app to Vercel. It was one of the easiest deployments I've done. While their interface is pretty intuitive and walks the user through steps, I decided to write up a step by step guide of my own experience.

- Sign up with the hobby (free) account by connecting Vercel to a git provider or email (I chose Github)
- Give access to vercel
- Add a phone number for a one time code
- Choose to import a git repository
- Select the correct organization
- Decide if you want all repo's imported, or certain ones
- If you are not an owner of the repo, you will be prompted to request access from an owner to connect the vercel and (in my case) Github organization
- Once the owner approves, the repo(s) should show up on your vercel dashboard
- Import the selected repo
- You will be forced to create a team since the selected repo belongs to a Github org (at the time this post was written, this will put you on a 14 day free Pro trial, so you don't have to pay immediately)
- Scroll to the "configure project" section
  - Name your project
  - The default "build and output settings" were fine in my use case
  - Click the "environment variables" dropdown and include the necessary variables
  - The values are all encrypted, so it's [safe to put secrets](https://vercel.com/docs/concepts/projects/environment-variables) here too!
- Press "deploy"

See you next time. 🙃
