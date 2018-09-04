---
title: GitHub pages
category: Jekyll
layout: 2017/sheet
---

## Custom domains

### Custom domains

```sh
$ echo "foobar.com" > CNAME
$ git commit && git push
```

Create a `CNAME` file with your domain on it.

See: [Setting up a custom domain](https://help.github.com/articles/quick-start-setting-up-a-custom-domain/) _(github.com)_

### Set up your domain

Subdomain (like www):
{: .-setup}

     CNAME => username.github.io

Apex domains:
{: .-setup}

     ALIAS => username.github.io

Apex domains (alternative):
{: .-setup}

    A => 192.30.252.153
    A => 192.30.252.154

### Serve Locally (windows)

_See -> [Setting up your GitHub Pages site locally with Jekyll - User Documentation](https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/)_

*  From the website's root dir: `bundle exec jekyll serve`


## References
{: .-one-column}

- <https://pages.github.com>
