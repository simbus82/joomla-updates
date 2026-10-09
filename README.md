# Joomla Updates — Simbus82

Public update server for the Joomla extensions by **Simbus82**.

This repository contains **only** what Joomla needs to notify and install updates:

- `updates/<extension>.xml` — the [Joomla update server](https://manual.joomla.org/docs/building-extensions/install-update/update-server/) file of each extension;
- the installable packages, attached to the [releases](../../releases) of this repository (tags `<extension>-v<version>`).

The source code of the extensions lives in their own repositories.

## Extensions

| Extension | Element | Update file | Joomla | PHP |
| :--- | :--- | :--- | :--- | :--- |
| SPPB AI MCP Bridge (MCP server for SP Page Builder) | `com_sppb_mcp` | [`updates/com_sppb_mcp.xml`](updates/com_sppb_mcp.xml) | 5.x, 6.x | 8.1+ |

## How it works

Each extension declares its update server in its manifest:

```xml
<updateservers>
    <server type="extension" priority="1" name="SPPB AI MCP Bridge">https://raw.githubusercontent.com/simbus82/joomla-updates/main/updates/com_sppb_mcp.xml</server>
</updateservers>
```

Joomla periodically reads that file. When it lists a version newer than the installed one, the update appears in **System → Update → Extensions** and can be installed with one click. Every package is published with its SHA-256 and SHA-512 checksums, which Joomla verifies before installing.

## Publishing a new version (maintainers)

Releases are published from the extension's own repository with its release script (for `com_sppb_mcp`: `npm run publish:update`). The script:

1. creates the release `<extension>-v<version>` here with the installable packages;
2. regenerates `updates/<extension>.xml` with version, download URL and checksums;
3. checks that the files are reachable anonymously and that the checksums match.

Do not edit the update files by hand.
