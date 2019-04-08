## Web hosting providers (FTP)

To upload a Jekyll site to a web host using FTP, simply run the `JEKYLL_ENV=production jekyll build` command and copy the generated `_site` folder to the root folder of your hosting account.

## GitHub Pages

**What are GitHub Pages?** <br> [GitHub Pages](https://pages.github.com/) are public web pages for users, organisations, and repositories, that are freely hosted on GitHub’s `github.io` domain or on a custom domain name of your choice.

**Full GitHub Pages deployment guide.** <br> We recommend you to read full GitHub Pages deployment guide [here](http://jekyllrb.com/docs/github-pages/).

>__Set relative URLs properly!__ <br> Please take a look at Relative URLs part of "Configuration" section before you deploy your site.

>__Build site with environment variable!__ <br> Please build your site with proper environment variable before you deploy. Your build command should look like this `JEKYLL_ENV=production jekyll build`.

### User and Organisation Pages

User and organisation pages live in a special GitHub repository dedicated to only the GitHub Pages files. This repository must be named after the account name. For example, [@mojombo’s user page repository](https://github.com/mojombo/mojombo.github.io) has the name `mojombo.github.io`.

Content from the `master` branch of your repository will be used to build and publish the GitHub Pages site, so make sure your `_site` directory content is stored there.

### Project Pages

Unlike user and organisation pages, project pages are kept in the same repository as the project they are for, except that the website content is stored in a specially named `gh-pages` branch or in a `/docs` folder on the `master` branch.

Content from the `gh-pages` branch or `/docs` folder on your `master` branch of your repository will be used to build and publish the GitHub Pages site, so make sure your `_site` directory content is stored there.

Output will become available under a subpath of your user pages subdomain, such as `username.github.io/project` (unless a custom domain is specified).

## GitLab Pages

**What are GitLab Pages?** <br> With [GitLab Pages](https://about.gitlab.com/features/pages/) you can create static websites for your GitLab projects, groups, or user accounts. Connect as many customs domains as you like and bring your own TLS certificate to secure them.

**Full GitLab Pages deployment guide.** <br> We recommend you to read full GitLab Pages deployment guide [here](https://docs.gitlab.com/ee/user/project/pages/).

>__Set relative URLs properly!__ <br> Please take a look at Relative URLs part of "Configuration" section before you deploy your site.

>__Build site with environment variable!__ <br> Please build your site with proper environment variable before you deploy. Your build command should look like this `JEKYLL_ENV=production jekyll build`.

### User and Organisation Pages

User and organisation pages live in a special GitLab repository dedicated to only the GitLab Pages files. This repository must be named after the account name.

For example, if you create a project called `john.gitlab.io` under your username, `john`, your project URL will be `https://gitlab.com/john/john.gitlab.io`. Once you enable GitLab Pages for your project, your website will be published under `https://john.gitlab.io`.

Content from the `gl-pages` branch of your repository will be used to build and publish the GitLab Pages site, so make sure your `_site` directory content is stored there.

### Project Pages

Unlike user and organisation pages, project pages are kept in the same repository as the project they are for, except that the website content is stored in a specially named `gl-pages` branch.

Content from the `gl-pages` branch of your repository will be used to build and publish the GitLab Pages site, so make sure your `_site` directory content is stored there.

Output will become available under a subpath of your user pages subdomain, such as `username.gitlab.io/project` (unless a custom domain is specified).
