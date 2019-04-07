<div class="container">

<div class="row">

<div class="col-md-7">

<div class="content">

## Introduction

`_config.yml` stores configuration data. Many of these options can be specified from the command line executable but it’s easier to specify them here so you don’t have to remember them.

<div class="callout callout--warning">

**Please stop and re-run `jekyll serve` command after you change configuration file!** Master configuration file contains global configurations and variable definitions that are read once at execution time. Changes made to `config.yml` during automatic regeneration are not loaded until the next execution.

</div>

## Relative URLs

If you’re deploying to server where your site is not going to be in `root` directory, you should setup `baseurl` variable.

For example, if your site is going to be stored on URL that looks like this `http://example.com/project`, you’ll have to update your `baseurl` variable and it should look like this:

<div class="language-yml highlighter-rouge">

<div class="highlight">

    snet:
    baseurl: /project

</div>

</div>

<div class="callout callout--warning">

**Build site with environment variable!** When you run `jekyll serve`, your `baseurl` variable shouldn’t render at all in any pages.

We’ll set Jekyll to only render `baseurl` variable when its environment is set to production.

So then, how do you get the `baseurl` variable to only show up on a production environment? When building your Jekyll project with jekyll build, you’ll want to prefix it with `JEKYLL_ENV=production` so the complete command looks like this one: `JEKYLL_ENV=production jekyll build`

</div>

## Color themes

The SingularityNET Developer Portal Theme supports a few color themes:

*   blue (default SingularityNET theme)
*   green
*   purple
*   red
*   yellow

You can update your `color_theme` variable in `_config.yml` to see changes.

<div class="language-yml highlighter-rouge">

<div class="highlight">

    snet:
    color_theme: green

</div>

</div>

## Header

### Logo with text

If you need logo as text, update `text` variable and leave `image` empty.

<div class="language-yml highlighter-rouge">

<div class="highlight">

    snet:
    header:
    logo:
        text: Project name
        image:

</div>

</div>

### Logo with image

If you need logo as image, update `image` variable and set it to `true` and leave `text` empty.

To set your custom logo image just upload it in place of `logo.png` here  
`/theme/assets/images/layout/logo.png`.

<div class="language-yml highlighter-rouge">

<div class="highlight">

    snet:
    header:
    logo:
        text:
        image: true

</div>

</div>

<div class="callout callout--info">

**Recommended logo image size.** Recommended logo image size is 400px x 178px. With this size you are sure you'll have retina ready logo image.

</div>

### Navigation

To add new items in main navigation you have to setup `nav` variable in `_config.yml`. Add as many items as you need.

<div class="language-yml highlighter-rouge">

<div class="highlight">

    snet:
    header:
    nav:
        - item_name: Item 1
          item_url: /example-url-1
        - item_name: Item 2
          item_url: /example-url-2

</div>

</div>

## Footer

### Logo with text

If you need logo as text, update `text` variable and leave `image` empty.

<div class="language-yml highlighter-rouge">

<div class="highlight">

    snet:
    footer:
    content:
        logo:
            text: Project name
            image:

</div>

</div>

### Logo with image

If you need logo as image, update `image` variable and set it to `true` and leave `text` empty.

To set your custom logo image just upload it in place of `logo-footer.png` here `/theme/assets/images/layout/logo-footer.png`.

<div class="language-yml highlighter-rouge">

<div class="highlight">

    snet:
    footer:
    content:
        logo:
            text:
            image: true

</div>

</div>

<div class="callout callout--info">

**Recommended logo image size.** Recommended logo image size is 400px x 178px. With this size you are sure you'll have retina ready logo image.

</div>

### Copyright

If you need to setup new footer copyright text, update `copyright` variable in your `_config.yml` file.

<div class="language-yml highlighter-rouge">

<div class="highlight">

    snet:
    footer:
    content:
        copyright: Copyright &copy; 2017\. - Project name <br>All rights reserved.

</div>

</div>

### Social list

To properly setup social list update `social_list` variable in `_config.yml`. Add as many items as you need.

At the bottom of the “Getting Started” section you can find a list of icons you can use in this list. Update `network_name` variable to add a proper icon.

<div class="language-yml highlighter-rouge">

<div class="highlight">

    snet:
    footer:
    social_list:
        - network_name: facebook
          profile_url: http://example.com
        - network_name: twitter
          profile_url: http://example.com
        - network_name: instagram
          profile_url: http://example.com
        - network_name: youtube
          profile_url: http://example.com

</div>

</div>

## Google Analytics

To activate Google Analytics you have to update `_config.yml` with GA tracking code. You can do that with `tracking_code` variable.

<div class="language-yml highlighter-rouge">

<div class="highlight">

    snet:
    google_analytics:
    tracking_code: UA-XXXXXX-X

</div>

</div>

<div class="callout callout--warning">

**Build site with environment variable!** When you run `jekyll serve`, your Google Analytics tracking code shouldn’t render at all in any pages.

The reason for this is if you visit your Google Analytics account, you’ll see a bunch of visits from `localhost:4000` or `127.0.0.1:4000` depending on the type of operating system you’re developing your Jekyll project on.

This can potentially muddy up your analytics, so to mitigate this problem, we’ll set Jekyll to only render Google Analytics when its environment is set to production.

So then, how do you get the analytics to only show up on a production environment? When building your Jekyll project with jekyll build, you’ll want to prefix it with `JEKYLL_ENV=production` so the complete command looks like this one: `JEKYLL_ENV=production jekyll build`

</div>

## Disqus comments

To activate Disqus commenting system you have to update `_config.yml` with the Disqus forum shortname. You can do that with `disqus_forum_shortname` variable.

Comments are available only on `default` page layout and you have to enable them on new pages with `comments: true` variable.

Currently, we have integrated Discourse comments into our SingularityNET Developer Portal which link directly to topics created on [our forum](https://community.singularitynet.io/c/developers).

<div class="language-yml highlighter-rouge">

<div class="highlight">

    snet:
    comments:
    disqus_forum_shortname:

</div>

</div>

<div class="callout callout--warning">

**Build site with environment variable!** When you run `jekyll serve`, your Disqus commenting system shouldn’t render at all in any pages.

We’ll set Jekyll to only render Disqus commenting system when its environment is set to production.

So then, how do you get the Disqus commenting system to only show up on a production environment? When building your Jekyll project with jekyll build, you’ll want to prefix it with `JEKYLL_ENV=production` so the complete command looks like this one: `JEKYLL_ENV=production jekyll build`

</div>

## Favicon

To change favicon just replace `/favicon.ico` with your new icon. Make sure it is in `.ico` format. Dimensions should be 16px x 16px.

<div class="callout callout--info">

**Favicon `.psd` file included!** We've included `.psd` file with pre-made favicon in `/designs` folder of your theme.

</div>

</div>

</div>

</div>

</div>
