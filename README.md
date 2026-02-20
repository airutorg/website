# airut.org Website

Public website for [Airut](https://github.com/airutorg/airut), a headless
Claude Code interaction system that operates through email and Slack.

**Live site:** [airut.org](https://airut.org)

## Example Project

This repository serves as a simple demonstration of the Airut
message-to-deploy workflow:

1. **Send a message** (email or Slack) to the Airut agent with your request
2. **Receive a response** with a Cloudflare Pages preview URL
3. **Review the PR** and approve to deploy to production

No local development environment needed. Just send instructions and get
working previews.

## Structure

```
public/           Static files served by Cloudflare Pages
  index.html      Landing page
  logo.svg        Airut logo
scripts/          Utility scripts (not published)
.airut/           Airut agent configuration
```

## Deployment

The site auto-deploys via Cloudflare Pages:

- Push to `main` → deploys to [airut.org](https://airut.org)
- Pull requests → preview URLs at `*.airut-website.pages.dev`

## Learn More

See the main [Airut repository](https://github.com/airutorg/airut) for
documentation on setting up agent workflows for your own projects.
