# cityu-ezproxy

A browser Redirector configuration for City University of Hong Kong (CityUHK) members to automatically route academic journal URLs through the CityU library EZproxy, enabling seamless off-campus access to subscribed databases.

![Workflow overview](asserts/workflow.png)

## What it does

### The problem

You're **off-campus**, you click on a paper link from Google Scholar, Twitter, or a colleague's email — and you land on the publisher's site staring at a **"Buy or subscribe"** paywall. Even worse, when you click "Access through your institution" and search for "City University of Hong Kong", the publisher's institution picker sometimes returns the wrong entry (e.g. *City University of Hong Kong (DongGuan)*), or fails to find CityU at all.

The conventional workaround is to use the CityU VPN, but **VPN doesn't actually solve this** — many publishers identify your institution by referrer/EZproxy URL, not by IP address, so you still see the paywall even when connected to VPN.

### The solution

This config makes your browser automatically rewrite publisher URLs to go through CityU's EZproxy. The rewrite happens silently in the background — you click a link, and you land directly on the full-text version with a **"You have full access to this article via City University of Hong Kong Library"** banner and a Download PDF button.

## Installation

### 1. Install the Redirector browser extension

- **Chrome / Edge**: [Redirector on Chrome Web Store](https://chromewebstore.google.com/detail/redirector/lioaeidejmlpffbndjhaameocfldlhin)
- or any other Redirector browser extension

### 2. Import the configuration

1. Download [`cityu_redirector.json`](./cityu_redirector.json) from this repo.
2. Click the Redirector icon in your browser toolbar → **Edit Redirects**.
3. Click **Import** at the bottom of the page.
4. Select the downloaded JSON file.
5. Make sure Redirector is **enabled** (toggle at the top).

### 3. Log in to CityU EZproxy once

The first time you visit any redirected URL, you'll be prompted to log in with your CityU EID and password. After that, your session is cached and redirects will work transparently.

## Who is this for

This is intended for **current CityU students, faculty, and staff** with valid library access. The EZproxy redirects only work if you can authenticate with the CityU library system.

## Customization

To disable a rule without deleting it, set `"enabled": false` in the JSON.

To add a new publisher, follow this pattern:

```json
{
  "enabled": true,
  "from": "^https://www.example-publisher.com/(.*)",
  "mode": "regex",
  "testUrl": "https://www.example-publisher.com/some/article",
  "to": "https://www-example-publisher-com.ezproxy.cityu.edu.hk/$1"
}
```