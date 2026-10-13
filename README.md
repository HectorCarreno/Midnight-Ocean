# Midnight Ocean

Midnight Ocean is a collection of four dark color themes for Visual Studio Code. Deep, low-glare backgrounds are paired with distinct ocean-inspired accents to make code, editor controls, and the surrounding workbench easy to scan.

## Choose a style

All four themes customize the editor and workbench, including the sidebar, tabs, activity bar, status bar, panels, inputs, buttons, selections, and integrated terminal. They also provide syntax colors for keywords, JSX tags, types, functions, strings, properties, numbers, and comments, with semantic highlighting enabled.

| Theme | Background | Palette |
| --- | --- | --- |
| **Midnight Ocean** | `#191923` | Ocean blue, sea-glass green, warm orange, and berry |
| **Midnight Ocean Dusk** | `#111827` | Sky blue, violet, mint, and golden yellow |
| **Midnight Ocean Reef** | `#081B1F` | Reef teal, bright cyan, mint, and yellow |
| **Midnight Ocean Ember** | `#17171A` | Icy cyan, violet, mint, and warm orange |

Types and numbers use warm accent colors; keywords, functions, and properties use each variant's brighter accents. Strings and comments use softer colors for contrast and visual hierarchy.

## Install the theme

### Install the latest release

Download the latest VSIX installer from the [GitHub Releases page](https://github.com/HectorCarreno/Midnight-Ocean/releases/latest), or use this direct download:

[Download the latest Midnight Ocean VSIX](https://github.com/HectorCarreno/Midnight-Ocean/releases/latest/download/midnight-ocean.vsix)

In VS Code:

1. Download `midnight-ocean.vsix` using the link above.
2. Open the **Extensions** view (`Ctrl+Shift+X`).
3. Open the **More Actions** menu (`...`) in the Extensions view and choose **Install from VSIX...**.
4. Select the downloaded `midnight-ocean.vsix` file.
5. Open the Command Palette (`Ctrl+Shift+P`), run **Preferences: Color Theme**, and select one of the four Midnight Ocean themes.

Alternatively, install it from a terminal with the [VS Code command-line interface](https://code.visualstudio.com/docs/editor/command-line):

```sh
code --install-extension ./midnight-ocean.vsix
```

### Build an installer from source

To package the current source instead of using the included VSIX, install [Node.js](https://nodejs.org/) and [pnpm](https://pnpm.io/), then run these commands from the project directory:

```sh
pnpm install
pnpm run package
```

The `package` script runs `vsce package --no-dependencies` and creates a versioned `.vsix` file in the project directory, such as `midnight-ocean-0.0.2.vsix`. Install that file using the VS Code steps above, or run `code --install-extension ./midnight-ocean-0.0.2.vsix`.

## Automated releases

Every push to `main` starts a GitHub Actions release workflow. It increments the patch version in `package.json`, commits that version bump to `main`, packages the extension, and creates a GitHub Release with both a versioned VSIX and a stable `midnight-ocean.vsix` download. The workflow requires repository Actions to have permission to write contents; branch protection must allow the workflow token to push the version-bump commit. Commits pushed with the workflow's `GITHUB_TOKEN` do not trigger another workflow run.

The workflow publishes GitHub Releases only; publishing to the Visual Studio Marketplace remains a separate, manual process.

## Activate or switch themes

After installation, open the Command Palette with `Ctrl+Shift+P` and select **Preferences: Color Theme**. Choose **Midnight Ocean**, **Midnight Ocean Dusk**, **Midnight Ocean Reef**, or **Midnight Ocean Ember**.

You can also set a theme directly in your VS Code `settings.json`:

```json
{
  "workbench.colorTheme": "Midnight Ocean Dusk"
}
```

Replace the value with the exact name of any of the other three themes to switch variants.

## Publish to the Visual Studio Marketplace

Publishing is optional. To make the extension available through the VS Code Extensions view:

1. Create or sign in to a Microsoft account and create a publisher in the [Visual Studio Marketplace publisher management portal](https://marketplace.visualstudio.com/manage). Note the publisher ID.
2. In `package.json`, replace the placeholder publisher value (`local-developer`) with your Marketplace publisher ID. Set the extension version to the version you intend to release. The publisher ID must match the publisher used to authenticate in the next steps.
3. Create an Azure DevOps personal access token with **Marketplace: Manage** scope. Keep the token private; do not add it to the repository.
4. From the project directory, install dependencies if needed and sign in to `vsce`:

   ```sh
   pnpm install
   pnpm exec vsce login <publisher-id>
   ```

   When prompted, enter the personal access token.

5. Publish the extension:

   ```sh
   pnpm exec vsce publish
   ```

   To publish a new version, first update the `version` in `package.json`, then run the publish command. `vsce publish` packages and uploads the extension to the Marketplace.

Once the Marketplace listing is available, users can search for **Midnight Ocean** in VS Code's Extensions view, install it, and choose their preferred variant as described above.
