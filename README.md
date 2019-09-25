# GitHub Actions for WordPress

GitHub actions for WordPress by different authors, and how to use them. Watch my talk on [WordSesh](https://WordSesh.com).

## [WordPress.org Plugin Deploy by **10up**](https://github.com/marketplace/actions/wordpress-plugin-deploy)

This action is triggered whenever a Git tag is released in your GitHub repository.
It automates the deployment of all the contents in the tag to the WordPress.org SVN repository.

### Triggers
Whenever a new tag is published.

### Usage

1. Inside your plugin repository on GitHub, create a `.github/workflows/deploy.yml` file.

2. Use this code:

``` bash
name: Deploy to WordPress.org
on:
    push:
        tags:
            - '*'
jobs:
    tag:
        name: WordPress.org Release
        runs-on: ubuntu-latest
        steps:
            - uses: actions/checkout@master
            - name: WordPress Plugin Deploy
              uses: 10up/actions-wordpress/dotorg-plugin-deploy@master
              env:
                  GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
                  SVN_PASSWORD: ${{ secrets.SVN_PASSWORD }}
                  SVN_USERNAME: ${{ secrets.SVN_USERNAME }}
                  SLUG: your-plugin-slug
```

3. If your GitHub repository slug is not same as the WordPress slug, add the
wordpress slug.

6. By default this actions pulls your assets from `.wordpress-org` folder in your GitHub repository.
You can either rename your current assets folder to `.wordpress-org` or customize it using
`ASSETS_DIR` variable.

4. Commit the file.

5. Go to your repository settings. In the Secrets tab, create two secrets
`secrets.SVN_PASSWORD` and `secrets.SVN_USERNAME` and add the credentials as their
values.

The action will run itself each time you tag a release 🎉

## [WordPress.org Plugin Readme/Assets Update by **10up**](https://github.com/10up/action-wordpress-plugin-asset-update)

This action will watch for any changes to readme.txt and plugin assets (Icons, Screenshots) on your Git repository and deploy them to the SVN repository. This action can also be run in tandem with the first Deploy Action.

### Triggers
With each push to the master branch that updates assets/readme. 

### Usage

1. Inside your plugin repository on GitHub, create a `.github/workflows/deploy.yml` file.

2. Use this code:

``` bash
name: Plugin asset/readme update
on:
  push:
    branches:
    - master
jobs:
  master:
    name: Push to master
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@master
    - name: WordPress.org plugin asset/readme update
      uses: 10up/action-wordpress-plugin-asset-update@master
      env:
        SVN_PASSWORD: ${{ secrets.SVN_PASSWORD }}
        SVN_USERNAME: ${{ secrets.SVN_USERNAME }}
        SLUG: your-plugin-slug
```

3. If your GitHub repository slug is not same as the WordPress slug, add the
wordpress slug.

6. By default this actions expects these assets to be in `.wordpress-org` folder in your GitHub repository.
You can either rename your current assets folder to `.wordpress-org` or customize it using
`ASSETS_DIR` variable after the slug variable.

4. Commit the file.

5. Go to your repository settings. In the Secrets tab, create two secrets
`secrets.SVN_PASSWORD` and `secrets.SVN_USERNAME` and add the credentials as their
values.

This action will run whenever you push changes to assets to master 🎉

## More Actions

### [PHPCS on pull request by rtCamp](https://github.com/rtCamp/action-phpcs-code-review)
### [Notify Slack with Deployment Status by rtCamp](https://github.com/rtCamp/action-slack-notify)
