# GitHub action to trigger a build in Netlify

Trigger a build on Netlify, if there's no site for this repo it can automagically set up one with the specified base directory, command, and publish directory.

## Secrets
- `GITHUB_TOKEN` - *Required* GitHub token provided by actions to validate requests
- `NETLIFY_SITE_ID` - *Optional* API site ID of the site you wanna work on
  [Obtain it from the UI](https://www.netlify.com/docs/cli/#link-with-an-environment-variable)

## Environment Variables
- `NETLIFY_BASE` - *Optional* Directory to change to before starting build
- `NETLIFY_CMD` - *Optional* Build command to build site
- `NETLIFY_DIR` - *Optional* The directory to publish (relative to root of your repo)

## Examples

Trigger a build to a specific site in Netlify

```hcl
workflow "Publish on Netlify" {
  on = "push"
  resolves = ["Publish"]
}

action "Publish" {
  uses = "netlify/actions/build@master"
  secrets = ["GITHUB_TOKEN", "NETLIFY_SITE_ID"]
}
```

Trigger a build on Netlify, if there's no site for this repo it will automagically set up one with the specified base, command, and publish directory.

```hcl
workflow "Publish on Netlify" {
  on = "push"
  resolves = ["Publish"]
}

action "Publish" {
  uses = "netlify/actions/build@master"
  secrets = ["GITHUB_TOKEN"]
  env = {
    NETLIFY_BASE = "site"
    NETLIFY_CMD = "npm build"
    NETLIFY_DIR = "site/_build"
  }
}
```
