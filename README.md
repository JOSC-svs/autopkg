# JetBrains Toolbox AutoPkg Recipes

AutoPkg recipes for downloading the latest stable Apple Silicon release of JetBrains Toolbox and importing it into a Munki repository.

## Recipes

- `JetBrainsToolbox.download.recipe` downloads the latest Apple Silicon DMG from JetBrains and verifies the application code signature.
- `JetBrainsToolbox.munki.recipe` imports the downloaded DMG into Munki.

## Requirements

- AutoPkg 2.4.1 or later
- Munki tools
- A configured Munki repository

These recipes are intended for Apple Silicon Macs. The generated Munki item is restricted to the `arm64` architecture.

## Usage

Add the recipe repository to AutoPkg, or place both recipe files in a directory included in `RECIPE_SEARCH_DIRS`.

Inspect the recipes:

```bash
autopkg info JetBrainsToolbox.download.recipe
autopkg info JetBrainsToolbox.munki.recipe
```

Test the download recipe without importing anything into Munki:

```bash
autopkg run JetBrainsToolbox.download.recipe -vv
```

Download and import JetBrains Toolbox into Munki:

```bash
autopkg run JetBrainsToolbox.munki.recipe -vv
```

## Munki Configuration

The following values can be customized in the `Input` dictionary of `JetBrainsToolbox.munki.recipe`:

- `NAME`
- `MUNKI_REPO_SUBDIR`
- `MUNKI_CATEGORY`
- `pkginfo`

By default, the recipe imports the item with these values:

| Setting | Value |
| --- | --- |
| Munki name | `JetBrainsToolbox` |
| Display name | `JetBrains Toolbox` |
| Repository subdirectory | `apps/JetBrainsToolbox` |
| Catalog | `testing` |
| Category | `Developer Tools` |
| Architecture | `arm64` |

Edit the `pkginfo` dictionary to change the description, developer, catalog, or other Munki metadata.

## Security

The download recipe validates the following before the application is imported:

- Code-signing identifier: `com.jetbrains.toolbox`
- JetBrains Team ID: `2ZEFAR8TH3`

The download URL is obtained from the official JetBrains release API.

## Recipe Identifiers

- `com.github.JOSC-svs.download.JetBrainsToolbox`
- `com.github.JOSC-svs.munki.JetBrainsToolbox`
