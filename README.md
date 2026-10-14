# My Blog

A small, public Jekyll blog with a browser-based writing editor. Posts are Markdown files in this repository; the editor saves them to GitHub, and GitHub Pages publishes the site.

## Set it up

1. Create a GitHub repository for the blog and add these files to its default branch (the editor is configured for `main`).
2. In `admin/config.yml`, replace `YOUR_GITHUB_USERNAME/YOUR_REPOSITORY` with the repository's `owner/name`.
3. If this is a project site at `https://OWNER.github.io/REPOSITORY/`, set `baseurl` in `_config.yml` to `"/REPOSITORY"` and set `public_folder` in `admin/config.yml` to `"/REPOSITORY/assets/uploads"`. For a user/organization site or custom domain, leave `baseurl` as `""` and keep `public_folder` as `"/assets/uploads"`.
4. In the repository's **Settings → Pages**, choose **Deploy from a branch**, select `main` and `/(root)`, then save. GitHub Pages will build the Jekyll site.
5. Open the published site and check that the home page and sample post load.

## Enable the editor

The editor is at `https://YOUR_SITE/admin/`. It uses GitHub login; only accounts with write access to the repository can publish. GitHub requires a server-side OAuth exchange, so the public site must not contain a GitHub token or OAuth client secret.

One straightforward setup is [Netlify's OAuth provider](https://docs.netlify.com/manage/security/secure-access-to-sites/oauth-provider-tokens/):

1. Create a Netlify site and configure its GitHub authentication provider using Netlify's instructions. The Netlify site can be used for authentication even if the public blog is hosted on GitHub Pages.
2. [Register a GitHub OAuth application](https://github.com/settings/developers). Set its callback URL to `https://api.netlify.com/auth/done`, then add its client ID and secret to the Netlify site's GitHub authentication provider settings. Keep the secret in Netlify; never put it in this repository.
3. Replace the repository placeholder in `admin/config.yml` and confirm `base_url: https://api.netlify.com` and `auth_endpoint: auth` are present.
4. Commit the configuration and wait for GitHub Pages to redeploy. Visit `/admin/`, sign in with a GitHub account that can write to the repository, create a post, and publish it.

With editorial workflow enabled, new posts are created as pull requests. Merge the post's pull request to publish it; GitHub Pages will rebuild the blog after the merge.

## Write without the editor

You can also add a Markdown file to `_posts/` using the filename format `YYYY-MM-DD-post-title.md`. Include front matter like this:

```yaml
---
layout: post
title: "My post title"
date: 2026-10-14 09:00:00 +0000
description: "A short summary shown on the home page."
---
```

Commit it to the branch selected in **Settings → Pages** to publish.
