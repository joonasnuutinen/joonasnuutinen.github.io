---
title: How to redirect a secondary domain to GitHub Pages
description: I redirected a secondary apex domain to my primary GitHub Pages domain. This is how.
date: 2023-10-16
tags:
  - coding
draft: true
---

I have registered two domains for myself: joonasnuutinen.com and joonasnuutinen.fi. The .com domain is the primary one and the .fi domain is a secondary one. As I recently [switched from WordPress to GitHub Pages](/blog/new-website), I had to come up with a new way to redirect traffic. Earlier my hosting provider supported secondary domains that redirect to the primary domain. In essence, I would just need to direct the secondary domain to my hosting provider's server and they would take care of it. However, GitHub Pages doesn't seem to support more than one domain.

I _could_ create a new GitHub Pages site, connect the secondary domain to it and handle the redirection client-side. However, I don't like the extra step of loading a web page to the browser and relying on JavaScript. Instead, I want the redirection to happen server-side.

So what I needed was a server to handle the redirection. There are obviously many ways to set up a server but I ended up using Google Firebase Hosting for it for the following reasons:

- I have used Firebase before and know my way around it.
- I already have a Firebase account.
- It's quick to set up.
- It's free.

So, here's what I did, step by step (I skipped step 1 because I already had an account):

## 1. Create a Firebase account

Go to [firebase.google.com](https://firebase.google.com/) and click Get started. Log in with your Google credentials.

## 2. Install Firebase CLI

Install the Firebase CLI as a global npm package:

```bash
npm install -g firebase-tools
```

## 3. Connect the Firebase CLI to your account

```bash
firebase login
```

You don't need to allow Firebase to collect CLI and Emulator Suite usage and error reporting information if you don't want to.

## 4. Initialise a Firebase project

```bash
mkdir firebase-redirect
cd firebase-redirect
firebase init
```

Select `Hosting: Configure files for Firebase Hosting and (optionally) set up GitHub Action deploys` and `Create a new project` when prompted. Type in a name for your project. For the other prompts, you can stick with the defaults.

## 5. Configure the redirection

Open the newly generated `firebase.json` and modify it as follows:

```json
{
  "hosting": {
    "public": "public",
    "ignore": [
      "firebase.json",
      "**/.*",
      "**/node_modules/**"
    ],
    "redirects": [{
      "source": "**",
      "destination": "https://your-domain-here.com",
      "type": 301
    }]
  }
}
```

The `301` type means a permanent redirect. If you want a temporary redirect, use `302` instead.

## 6. Deploy to Firebase

```bash
firebase deploy
```

## 7. Configure DNS settings (apex domain)

- Go to the [Firebase Console](https://console.firebase.google.com/) and select the correct project.
- From the left navigation, go to Hosting.
- Click Add custom domain.
- Type in the apex (non-www) domain you want to redirect from.
- Leave the Redirect checkbox unchecked because redirection is configured in `firebase.json`. Click Continue.
- Set up the A and TXT records to your DNS as instructed and click Verify. You may need to wait for a couple of hours for the changes to take effect. You can close the dialog and retry verification later.

## 8. Configure DNS settings (www domain)

It's a good practice to redirect also the www domain because some of your visitors will likely include www in the address. You can do this while waiting for the verification in the previous step to succeed.

- Add a another custom domain.
- Type in the www domain you want to redirect from.
- This time select the Redirect checkbox and type in the same domain without www. Click continue.
- Set up the CNAME record to your DNS as instructed and click Verify. Again, you might need to wait for a couple of hours and try later.

## Conclusion

That's it! You should now be redirected from the secondary domain to the primary domain. If you want to take a look at my actual Firebase project in all its simplicity, [go here](https://github.com/joonasnuutinen/joonasnuutinenfi-redirect).