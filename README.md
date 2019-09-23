# GitHub Actions for WordPress

GitHub actions for WordPress by different authors, and how to use them.

## [WordPress.org Plugin Deploy by **10up**](https://github.com/marketplace/actions/wordpress-plugin-deploy)

This action is triggered whenever a Git tag is released in your GitHub repository.
It automates the deployment of all the contents in the tag to the WordPress.org SVN repository.

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

4. Commit the file.

5. Go to your repository settings. In the Secrets tab, create two secrets
`secrets.SVN_PASSWORD` and `secrets.SVN_USERNAME` and add the credentials as their
values.

6. By default this actions pulls your assets from `.wordpress-org` folder in your GitHub repository.
You can either rename your current assets folder to `.wordpress-org` or customize it using
`ASSETS_DIR` variable.

The action will run itself each time you tag a release 🎉
