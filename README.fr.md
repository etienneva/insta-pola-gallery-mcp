<p align="center"><img src="icon.png" width="96" alt="Insta-Pola"></p>

# Serveur MCP Insta-Pola

**Crée ta galerie photo d'évènement depuis ton assistant IA.**

[Insta-Pola](https://www.insta-pola.com) crée des galeries photo partagées pour les mariages, anniversaires, soirées et évènements d'équipe. Les invités scannent un QR code, postent leurs photos depuis leur téléphone (sans application ni compte) et les voient apparaître en direct sur un mur projeté dans la salle. Chaque photo devient un polaroid avec un titre, écrit par l'invité ou proposé par l'IA.

Ce serveur [MCP](https://modelcontextprotocol.io) distant permet à l'organisateur de créer et gérer ses galeries en langage naturel, depuis Claude, ChatGPT ou tout client MCP :

> « Crée une galerie photo pour l'anniversaire de Léa samedi et donne-moi le QR code »
> « Renomme-la "Léa a 30 ans", mets-la en rose avec une police moderne »
> « Liste mes galeries et dis-moi combien de photos ont été postées »

🇬🇧 [English version](README.md)

## Adresses

Le serveur est hébergé par Insta-Pola : rien à installer.

| Client | URL | Outils |
|---|---|---|
| Claude (claude.ai, application, Claude Code) et autres clients MCP | `https://www.insta-pola.com/mcp/claude` | 4 |
| ChatGPT | `https://www.insta-pola.com/mcp` | 5 (avec `set_gallery_logo`) |

Transport Streamable HTTP, sans état. Inscrit au registre officiel MCP sous `com.insta-pola/photo-gallery`.

## Ajouter Insta-Pola à Claude

1. Ouvre **Personnaliser › Connecteurs**, puis **Ajouter un connecteur personnalisé**.
2. Nom : `Insta-Pola`. URL : `https://www.insta-pola.com/mcp/claude`
3. Si Claude demande un client OAuth, choisis **Enregistrer automatiquement**.
4. Clique sur **Connecter**, connecte-toi à ton compte Insta-Pola et clique sur **Autoriser**.
5. Dans une conversation, active Insta-Pola dans **+ › Connecteurs**.

Dans Claude Code :

```bash
claude mcp add --transport http insta-pola https://www.insta-pola.com/mcp/claude
```

Autres clients : voir [`examples/`](examples). Détails des outils, de l'authentification et des limites : [README en anglais](README.md).

## Support

- Documentation : https://www.insta-pola.com/site/assistant-ia.html
- Support : https://www.insta-pola.com/site/support.html · etienne@insta-pola.com

Insta-Pola est édité par Racine de E (France).
