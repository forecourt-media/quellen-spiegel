# quellen-spiegel

Spiegel **unveränderter** Upstream-Dateien, die die Builds von Forecourt Media laden (Issue
forecourt-media/forecourt-platform#652). Jede Datei liegt als Release-Asset unter einem Tag `<name>-<version>`.

Vertrauensanker ist **nicht** dieser Spiegel, sondern die im verbrauchenden Dockerfile gepinnte SHA-256: Die Builds
laden zuerst von hier, prüfen die Prüfsumme und fallen bei Fehler oder falscher Prüfsumme auf die Upstream-Quelle
zurück; stimmt keine Quelle, bricht der Bau ab.

| Tag | Datei | SHA-256 | Upstream |
|---|---|---|---|
| `ffmpeg-9.0.2` | `ffmpeg-9.0.2.tar.xz` | `8c3850283eb25fa026482078a04051e0be17347b09ef81a0849bec15a96e002e` | https://ffmpeg.org/releases/ (Signatur FCF9 86EA 15E6 E293 A564 4F10 B432 2F04 D676 58D8, geprüft 20.10.2026) |
| `node-v22.23.4` | `node-v22.23.4-linux-x64.tar.xz` | `1805bcd35e6815559bd2eb97db438d3fdb0eb3a5e6a977b7c1badca76337e9ce` | https://nodejs.org/dist/v22.23.4/ |

Lizenzen: die Dateien sind unverändert; die Lizenztexte liegen jeweils im Archiv (FFmpeg: LGPL/GPL, `COPYING.*`;
Node.js: `LICENSE`).

Neue Datei aufnehmen: von Upstream laden, SHA-256 gegen den Pin im verbrauchenden Repo prüfen, erst dann
`gh release create <tag> <datei> --notes "SHA-256 …"`. Assets nie ersetzen; neue Version = neuer Tag.
