<p align="center"><img src="logo.svg" width="72" alt="sharepa logo"></p>

# sharepa MCP connector

Turn pages and artifacts built in Claude, ChatGPT or any MCP client into working websites: your own address, forms that collect entries, bookings straight into your Google Calendar, an optional password and visit statistics without cookies.

More than HTML hosting: a landing page with a sign-up form, a booking page for first calls or a password-protected offer for a client, all published and updated from the chat.

sharepa is a hosted, remote MCP server. There is nothing to install or run. Add the server URL to your MCP client, sign in with your email, and ask your chat to publish.

```
https://app.getsharepa.ch/mcp
```

- Website: https://getsharepa.ch
- Setup guide: https://getsharepa.ch/en/guides/mcp-connector
- Listed in the official MCP Registry as `ch.getsharepa/sharepa` (see [`server.json`](server.json))

This repository contains the documentation and the registry metadata for the connector. The server itself is operated by sharepa and is not open source.

## What it does

Ask your chat to publish an HTML page or a React artifact and you get a link like `name.sharepa.page` within seconds. Later changes go to the same address. Forms on the page store their entries for you, and booking pages show free times from your Google Calendar and add booked appointments to it.

From the chat you can:

- publish a new page or a new version of an existing one (HTML or React, including Tailwind and common libraries)
- protect a page with a password, change it, or make the page public again
- connect your own subdomain, for example `offers.example.com`, with two DNS records
- see how a page is doing: daily visits, referrers and countries, counted on the server without cookies or IP addresses
- fetch the source of a published page to keep working on it
- collect form entries (contact, sign-up, waiting list); the owner reads them in the sharepa app
- take bookings in your Google Calendar on a page (one-time plan, currently in beta)

## Connect

**Claude** (claude.ai, Claude Desktop): Settings › Connectors › Add custom connector, name `sharepa`, URL `https://app.getsharepa.ch/mcp`, then Connect.

**ChatGPT**: enable developer mode, then add a connector with the URL above.

**Claude Code**:

```
claude mcp add --transport http sharepa https://app.getsharepa.ch/mcp
```

**Cursor, VS Code, LM Studio and others**: add a remote server with streamable HTTP and the URL above.

Step-by-step instructions with screenshots: https://getsharepa.ch/en/guides/mcp-connector

## Authentication

OAuth 2.0 with dynamic client registration. Metadata at `https://app.getsharepa.ch/.well-known/oauth-authorization-server`. You sign in with a one-time code sent to your email; there is no password. Scopes are `pages:read` and `pages:write`, and you can grant read-only access on the consent screen.

## Tools

| Tool | What it does | Writes |
|---|---|---|
| `list_pages` | Lists your pages with title, address, password and visits | no |
| `publish_page` | Publishes a new page or a new version of an existing one | yes |
| `prepare_upload` | Returns a one-time upload link for pages too large to pass as code | yes |
| `get_page_stats` | Daily visits, referrers, campaigns and countries of a page | no |
| `get_page_source` | Source code of the current version of a page | no |
| `set_password` | Sets, changes or removes a page password | yes |
| `connect_domain` | Connects your own domain or subdomain and returns the DNS records | yes |
| `list_booking_types` | Shows whether bookings are enabled and which booking types exist | no |
| `set_booking_type` | Creates or changes a booking type | yes |
| `set_page_booking` | Chooses which booking types a page offers | yes |

Nothing can be deleted through the connector. Deleting pages, disconnecting domains and reading form entries happen in the sharepa app.

## Example prompts

- "Build a landing page for my bakery with a contact form and publish it with sharepa."
- "List my sharepa pages."
- "How is my bakery page doing this week?"
- "Protect that page with a password."
- "Get the source of my budget calculator, change the currency to EUR and publish the new version."
- "I want the bakery page under bakery.example.com."

Name sharepa in the prompt; otherwise the chat may offer its own sharing instead.

## Privacy and security

- New pages are open to anyone with the link and hidden from search engines.
- Pages cannot send data to other servers: forms and requests only reach the page itself and sharepa.
- Visits are counted on the server without cookies, scripts or IP addresses.
- Data is stored with Cloudflare in the EU. sharepa is run from Switzerland.

Privacy policy: https://getsharepa.ch/en/datenschutz

## Plans

Free: three pages with a sharepa address. One-time plan: more pages, several pages on one domain, webhooks for form entries and bookings (beta). Details: https://getsharepa.ch/en/einmal-plan

## Support

konrad@getsharepa.ch
