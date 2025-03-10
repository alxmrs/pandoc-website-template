---
title: An Authenticated Content Management System with Decap and Cloudflare
date: 2025-03-09 5:10PM
meta-keywords: 
  - CMS
  - Cloudflare
  - Decap
  - authentication
  - OAuth
  - Static Site Generator
---

I'm revamping this template. One new feature that I thought would set it apart was an integration with a [git](https://git-scm.com/)[^1]-based content management system (AKA – a "CMS").

In the past, I've used Netlify CMS, which recently has been rebranded to ["Decap CMS."](http://decapcms.org/) A rose by any other name still posts as sweet. It was pretty nifty before, so I decided to re-use it again.

Setting up this CMS so far has been a piece of cake. It seems to integrate really well into pandoc's [default HTML5 template](https://github.com/jgm/pandoc-templates/blob/master/default.html5), which are configurable by [embedded YAML blocks](https://pandoc.org/MANUAL.html#extension-yaml_metadata_block). It turns out I can easily set "Decap [collections](https://decapcms.org/docs/configuration-options/#collections)" to write to these metadata blocks, and thus make it really easy to add and edit webpages! (Well, I haven't gotten this working all the way, but that's the hope.) The current missing piece for me is to get authentication set up, which requires some webservice (i.e. a tiny dynamic component of this otherwise static website).

Getting authentication and authorization is a serious matter. I want to make sure that only the people I allow to can edit this website ("authorization"). To that end, I need to make sure that the person with access is really who they say they are ("authentication"). I wouldn't want an adversary to be able to edit or delete a webpage that was valuable to me.

Luckily, I don't have to write a significant amount of code to accomplish this, thanks to the [OAuth standard](https://en.wikipedia.org/wiki/OAuth). To get up-and-running fast, I've decided to use GitHub – who hosts this website and manages its source code – to be my OAuth provider.

Here's what I did — and you can, too — to get auth set up.

> **Pre-requisites**: You need to have domain names managed in [Cloudflare](https://cloudflare.com/). This requires setting up an account and either [purchasing](https://www.cloudflare.com/products/registrar/) or [transferring](https://developers.cloudflare.com/registrar/get-started/transfer-domain-to-cloudflare/) domains over there. This is beyond the scope of this post.

1. I downloaded this [ready-to-go authentication proxy](https://github.com/sterlingwes/decap-proxy/) (provided by Decap).
   As a technical person, I "cloned the repository," but if you're not (but, open-minded to being slightly technical), then you can click the green "code" button and then click the option to download a Zip file. From there, you can unpack the zip to get a directory of source code and documentation.
2. I [followed the instructions](https://github.com/sterlingwes/decap-proxy/tree/main?tab=readme-ov-file#getting-started) to create a GitHub OAuth app. I chose "auth.merose.com" for my application URL, because this demo site is hosted as a subdomain of merose.com. I thought it was fitting. Since my site isn't private, I didn't have to modify any code. (I did not choose "device flow" because this site is focused on being managed on the web, not a device.)
3. I modified the "wrangler.toml" (including renaming the file) as instructed, using the target auth domain. Then, I logged in and deployed the proxy. I hadn't used `npm` in a while, so I had to update to the latest long-time-support version via `nvm`. If these are strange acronyms to you, but you want to follow along and are willing to copy & paste stuff into your computer's terminal (_it's generally not recommended to run code you read about on the internet! Viewer discretion is advised!_), first you need to download Node.JS: [nodejs.org/en/download/](https://nodejs.org/en/download/). After you have node set up locally ("Node" is just "Javascript" that runs outside your web browser), you can follow the Decap proxy instructions to call the Cloudflare function-as-a-service command-line tool, known as "wrangler." When you run `npx wranger login`, it tells your local terminal (and computer) to log into Cloudflare. When you run `npx wrangler deploy` inside of the root directory of the source code you downloaded in step (1), it will deploy that code (with the proper configuration) to Cloudflare.
4. From the GitHub app panel, I generated a new secret key and gathered my client ID. I followed instructions for passing this to my deployed app, which for me, meant running the two wrangler commands provided. 
5. I edited the `config.yml` file in the `admin/` directory of this template to use "https://auth.merose.com" as a `base_url` for the [Decap backend](https://decapcms.org/docs/choosing-a-backend/).

And that is it! From here, I plan to contribute this feature to my template. As of writing I'm not sure if this works, but my hope is that with a little tweaking, the next post of this blog will be written from the web!

[^1]: git is a piece of software to manage versions of documents or code in a decentralized manner.