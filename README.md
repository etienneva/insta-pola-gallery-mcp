<p align="center"><img src="icon.png" width="96" alt="Insta-Pola"></p>

# Insta-Pola MCP server

**Create shared event photo galleries from your AI assistant.**

[Insta-Pola](https://www.insta-pola.com) creates shared photo galleries for weddings, birthdays, parties and team events. Guests scan a QR code, post their photos from their phone (no app, no account) and see them appear live on a wall projected in the room. Each photo becomes a polaroid with a title, written by the guest or suggested by AI.

This remote [MCP](https://modelcontextprotocol.io) server lets an organizer create and manage their galleries in plain language from Claude, ChatGPT or any MCP client:

> "Create a photo gallery for Lea's birthday party next Saturday and give me the QR code"
> "Rename it 'Lea turns 30', make it pink and use a modern font"
> "List my galleries and tell me how many photos were posted"

🇫🇷 [Version française](README.fr.md)

## Endpoints

The server is hosted by Insta-Pola, so there is nothing to install or run.

| Client | URL | Tools |
|---|---|---|
| Claude (claude.ai, desktop, Claude Code) and other MCP clients | `https://www.insta-pola.com/mcp/claude` | 4 |
| ChatGPT | `https://www.insta-pola.com/mcp` | 5 (adds `set_gallery_logo`) |

- Transport: Streamable HTTP, stateless, JSON responses.
- Official MCP Registry: [`com.insta-pola/photo-gallery`](https://registry.modelcontextprotocol.io/v0/servers/com.insta-pola%2Fphoto-gallery/versions/latest)
- Gallery content and tool replies are in French.

## Setup

### Claude (claude.ai or the Claude app)

Insta-Pola is listed in the [Claude connectors directory](https://claude.ai/directory/connectors/insta-pola-photo-gallery).

1. Open the listing, or go to **Customize › Connectors** and search for **Insta-Pola**.
2. Click **Connect**, sign in to your Insta-Pola account and click **Autoriser** (Authorize).
3. In a conversation, enable Insta-Pola under **+ › Connectors**.

As a custom connector instead: **Add custom connector** with the URL `https://www.insta-pola.com/mcp/claude`; if Claude asks for an OAuth client, choose **Register automatically**.

On Claude Team or Enterprise, an organization owner adds the connector; each member then connects their own Insta-Pola account.

### Claude Code

```bash
claude mcp add --transport http insta-pola https://www.insta-pola.com/mcp/claude
```

### ChatGPT

The **Insta-Pola Photo Gallery** app is being published in the ChatGPT app directory.

### VS Code, Cursor and other clients

See [`examples/`](examples). Your client opens the Insta-Pola sign-in page on first use.

## Tools

| Tool | What it does | Annotations |
|---|---|---|
| `create_gallery` | Creates a gallery: `name`, `date` (YYYY-MM-DD), optional `private` (guest code), `theme`, `font`. Returns the guest link, QR code, live wall link and organizer links. | write, open world |
| `update_gallery` | Changes the `title`, `theme` or `font` of a gallery (`slug`). The gallery address does not change. | write, destructive (overwrites settings) |
| `list_galleries` | Lists the galleries of the connected account with their status. | read-only |
| `get_gallery` | Details of a gallery (`slug`): status, links, QR code, number of photos, logo guidance. | read-only |
| `set_gallery_logo` | ChatGPT only: sets an image from the conversation as the gallery logo (resized to 512 px). | write, destructive |

**Themes:** rose-editorial, corail-pastel, framboise-sorbet, peach-cream, mint-museum, mint-fresh, vert-sauge, vert-profond, bleu-petrole, bleu-nuit, bleu-glacier, beige-sable, moka-latte, sunrise-gold, chaplin-gold, citrus-pop, apricot-glow, saffron-night.

**Title fonts:** monoton, playfair, dmserif, lora, dancing, lobster, montserrat, robotoSemi, bitcount.

## Authentication and privacy

- OAuth 2.1 with PKCE (S256) and Dynamic Client Registration (RFC 7591); no client ID or API key to configure.
- Protected resource metadata (RFC 9728): [`/.well-known/oauth-protected-resource/mcp/claude`](https://www.insta-pola.com/.well-known/oauth-protected-resource/mcp/claude) and [`/.well-known/oauth-protected-resource`](https://www.insta-pola.com/.well-known/oauth-protected-resource).
- Discovery and the tool list are public. Every tool call requires a connected Insta-Pola account and only acts on that account's galleries.
- You can revoke access at any time from your assistant's settings or by contacting support.
- [Privacy policy](https://www.insta-pola.com/site/Politique-de-confidentialite.html) · [Terms](https://www.insta-pola.com/site/conditions.html)

## Limits

- 5 gallery creations per account per 24 hours; event date at most 90 days ahead.
- The first gallery of an account is free and goes live immediately. Additional galleries are created as drafts and are activated on insta-pola.com. The MCP server never handles payments.
- Photo moderation, album download, the welcome text, the logo (outside ChatGPT) and the printed souvenir book are managed on insta-pola.com; the tools return the right links.

## Support

- Documentation: https://www.insta-pola.com/site/assistant-ia.html
- Support: https://www.insta-pola.com/site/support.html · etienne@insta-pola.com
- Issues and suggestions: open an issue in this repository.

This repository documents the hosted server; the server source code is not published here.

[![Listed on mcpservers.org](https://mcpservers.org/badge.svg)](https://mcpservers.org/servers/etienneva/insta-pola-gallery-mcp)

Insta-Pola is published by Racine de E (France).
