![Tyton](assets/icon.png)

# Tyton for Claude

Tyton helps you get Meta Pixel and the Meta Conversions API (CAPI) working on your website, with Claude doing the setup alongside you.

- **Free audit**: Claude checks a public website's Meta tracking and tells you, in plain words, what works, what's missing and what it couldn't confirm. No account needed.
- **Setup**: Claude connects to one website in your Tyton account, guides you through Meta one step at a time, saves your Conversions API token safely, and installs only the conversions you approve. Tyton hosts the server that sends your events to Meta. The Free plan covers 1 site and 10,000 events a month (browser and server copies each count), with no card needed.

Learn more at [usetyton.com](https://usetyton.com) and in the [docs](https://usetyton.com/docs).

## What's in the plugin

- A connection to Tyton's server at `https://mcp.usetyton.com/mcp`.
- Three skills:
  - `meta-tracking-audit` runs the free audit and explains the result.
  - `meta-tracking-setup` handles sign-in, setup progress, Meta guidance and approvals.
  - `conversions-api-token` keeps your Meta token out of the chat, your code and your reports.

The plugin has no scripts, hooks or local programs. It works in Claude Code, on claude.ai and in Cowork.

## Install

In Claude Code:

```
/plugin marketplace add usetyton/tyton-plugin
/plugin install tyton@usetyton
```

On claude.ai or in Cowork, open **Customize > Plugins**, choose **Add**, then **Add marketplace**, and enter `https://github.com/usetyton/tyton-plugin`. Install Tyton, then connect it from the plugin's **Connectors** tab. Once Tyton is listed in the plugin directory, you can install it from there instead.

Then ask Claude something like "Audit the Meta tracking on my website" or "Set up Meta tracking for my site with Tyton".

## How sign-in works

The free audit needs no sign-in. For setup, Claude uses Sign in with Tyton:

1. When Claude first needs your site, your app shows a Connect or sign-in prompt for Tyton. In Claude Code you can also run `/mcp` and choose Tyton.
2. At usetyton.com you sign in or create an account, pick the Free plan or a paid one, and choose the one website Claude may work on.
3. You approve the connection. Claude can then read and change setup for that website only.

Connecting doesn't approve any tracking. Claude shows you the conversions it plans to track and waits for your clear yes before approving them. You can review or remove access any time on the **Integrations** page in Tyton.

## What data goes to Tyton

The plugin talks only to `mcp.usetyton.com`. Depending on what you ask for, Claude sends:

- **Audit**: your website URL, page HTML Tyton fetches or Claude supplies with your permission, Claude's findings about your tracking, and your answers to audit questions.
- **Setup**: your website URL, your Meta Pixel ID, your conversion plan and approvals, and setup test results.
- **Conversions API token**: only if you choose to save it through Claude. Tyton encrypts it and never shows it again. The Tyton browser extension can seal it first so the raw token never appears in the chat.

Claude is told never to send passwords, customer records, private source code or other personal data to audit tools. See the [privacy policy](https://usetyton.com/privacy) and the [terms](https://usetyton.com/terms).

## Support

Email [hello@usetyton.com](mailto:hello@usetyton.com) or read the [troubleshooting guide](https://usetyton.com/docs/troubleshooting).

## License

MIT. See [LICENSE](LICENSE).
