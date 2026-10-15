---
type: llm
weight: 2
---

PASS if the reply tells the customer to connect or sign in with Tyton (for example through the app's Connect or sign-in prompt, /mcp in Claude Code, or the plugin's Connectors tab), says they sign in at usetyton.com, pay only if needed and choose or approve the one website, and says setup continues once they are connected.

FAIL if it asks the customer to paste a server key, pairing code or password into the chat, shows a poll token, claims tracking is already set up, says that connecting approves tracking, or makes up a Pixel ID.
