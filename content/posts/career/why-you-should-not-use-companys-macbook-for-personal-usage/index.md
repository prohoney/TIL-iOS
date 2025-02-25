---
title: "Separate Devices, Better Life: Why Personal Freedom Beats Using Your Work MacBook"
date: 2024-12-18T18:10:19-05:00
category: [career]
tags: [career, life, MacBook, focus]
description: "Why having your own personal laptop is a game changer"
editPost:
    URL: 'https://github.com/mfaani/mfaani/tree/main/content'
    Text: Suggest Changes
    appendFilePath: true
---

<!-- Image prompt: Create a wide image of a person being stunk down into water due to the heavy weight of their MacBook. A chain is connecting the person's leg to the MacBook. The screen is showing Jira (the project management app). Add very few fish and shark into the water.!-->



# Pros

## Performance
- Company keeps adding more monitoring. Your MacBook will only get slower. You will get annoyed by this. 

!["slow MacBook"](slow.png "Mike Zorn's comment about this post")

- Apple is finding more ways to restrict access to surveillance. This forces companies to restrict access to tools further because they lack the visibility into things. *You* pay the price...
- Often developers get even restricted from using tools like Charles Proxy / Proxyman, because they require adding a new root certificate which then interfere with company's monitoring tools.
- You can leave your work laptop at work. Never carry it back and forth with yourself. Go easy on your back. Read a book, breath fresh air, make a friend. I find this to be significantly refreshing. I don't get when  people carry heavy laptops back and forth with zero usage at home. Your office should be treated as a safe as your home. 
- There's a ton of stuff that you 1) you must use a laptop. Can't use your iPhone for 2) absolutely don't want done with your work laptop. 
    - Doing your taxes
    - Applying and interviewing at other companies
    - Screen Recording and sharing. You don't want to be accidentally sharing something that was your company's sensitive data. 

> Your company's intent might just be compliance. But the affect on you is the same

## Complexities with having different accounts accounts
- You can't be sharing your Wallet, Photos, Contacts, Notes, Reminders. It's because iCloud from your personal iPhone with your Company's MacBook are likely to be with different Apple IDs.
- Configuration of certain developer or app become difficult as well if you want to separate work and personal things. Example:
    - Configuring multiple GitHub accounts and then making sure every commit is using the correct name and email can be done incorrectly without anyone noticing it.
- You can't use [Apple Handoff](https://support.apple.com/en-us/102426) between work Laptop and personal device i.e. you can't start work on one device, then switch to another nearby device and pick up where you left off.

That said someone gave feedback that he gets things across devices by: 

> Separate iCloud accounts and purchases are shared via family sharing

So maybe you can get around this by creating a dummy child account...


## Privacy
Assume the worst!

- 99% of what you do is likely recorded. Your email user/password all get logged and stored for however long your company's complain policy requires and more. While _most_ companies don't have keylogger, your user / pass is likely still exposed, because your company has root certificates installed and everything you send to the internet gets signed with it and therefore visible. Having an HTTPS or End to End encryption will **not** protect you from this, because their root certificate becomes part of the root chain.
- Unlikely, but company can profile you based on your network activity. 
- Less stress when leaving company. Because you don't have anything personal on it to transfer or lose. Last thing you want is a weirdo across the planet having hold of your family photos.

> You **never** know when they’ll lay you off and you lose access 😔.

- IT may have remote access capabilities to view your screen or take control without notification
- File sync services (Dropbox, Google Drive etc.) could potentially expose personal files to company monitoring or you may just be completely banned from using.

## Freedom
- Ability to work on side projects (or actual read personal projects). Your own app, blog or business. Not having your laptop can be extremely limiting.
- You can customize the specs and color however you like. You no longer need to select from company storage.
- There are no travel regulations for personal laptops.
- You can update to the latest Operating Systems or use Beta versions. 
- You can install any app you want. At work, I once created a fresh "Command Line Tool" app using Xcode. It was nothing but a dummy print "Hello World". The app crashed on launch because it was flagged by IT. 
- No Risk of Company Wiping Data.
- Freedom from Work-Required Apps.
- No need to change / set your password based on company's policy
- If you're a gamer then you can't install games on it. 
- Access to all the free internet. Some companies have banned access to ChatGPT or certain other websites. 
- Your favorites folder, the main apps you use can be very different across the two laptops.

## Focus
- It makes it very difficult to focus on life while at work or vice versa. Having two laptops makes focusing a lot easier. Once you allow receiving iMessages, emails on your work Laptop, then you've opened the Pandora's box. It just psychologically reinforce boundaries, signaling to your brain when to work and when to relax.
- Getting away from work truly happens when the laptop you're using after hours isn't your work device.
- Having separate devices helps maintain different browser bookmarks/history which aids context switching. Your work laptop could have a YouTube feed that's all about Technology, while your personal one is all about news, food, movies. 
- When you go on a vacation then you'd only be taking your personal laptop and ditch work entirely. 

## Clarity and Vision
Before getting my personal MacBook, my thoughts were consumed by work. Now, I feel free, unclipped and unchained. My perspective has completely shifted.

> It’s like owning a bike, you rarely consider traveling to a different state for fun. But with a car and a tent, you suddenly imagine endless possibilities and adventures.

# Cons
- Extra cost of device and purchasable apps.
- On trips you may need to carry two devices. I'm using 14" so it's easier for me. 
- Need to re-install and re-configure all your terminal aliases, git aliases, computer settings, IDE settings, SSH keys and access tokens, Networking configurations
