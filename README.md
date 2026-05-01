# AI & Biodiversity Change Global Center Catalog

Repository for web-based ABC Center code, data, model, and spaces catalog. This catalog is designed to use the GitHub API for searching all code repositories created under the [ABC GitHub Organization](https://github.com/ABC-Center) and the Hugging Face API for searching all dataset, model, and spaces repositories created under the [ABC Hugging Face Organization](https://huggingface.co/ABC-Center). Non-ABC Org GitHub repositories can be manually included through the `ADDITIONAL_REPOS` parameter in the [config file](public/config.yaml). 

This repository was generated and personalized from the [Imageomics Catalog](https://github.com/Imageomics/catalog). The following sections are pulled from the source repo.

## Features

The website is styled using the [tailwindcss](https://tailwindcss.com/) package.

* **Real-time Data Fetching:** Displays all public Imageomics repositories, fetched through the GitHub and Hugging Face APIs. Includes semantically meaningful virtual markers:
    * "New" badge highlights products created within the last 30 days;
    * "🚀 version-tag" badge indicates a new release within the last 2 weeks for GitHub repos, and links to that release;
    * Star (⭐️) or like (❤️) counts displayed for GitHub or Hugging Face repos, respectively;
    * Archived badge flags GitHub repos no longer under active development (read-only).
* **Search Functionality:** Quickly find items by keyword.
* **Filtering:** Filter by repository type (Code, Datasets, Models, Spaces) and tags. Optionally include archived GitHub repos.
* **Sorting:** Sort items by last updated, date created, stars/likes ascending or descending, or alphabetically.
* **URL Parameter Support:** Persist and share search states via URL hash (`#type=datasets&q=fish`) or query parameters (`?type=datasets`). Supports `type`, `q` (search query), `sort`, and `tag` parameters.
* **Responsive Design:** The layout is optimized for use on computers and mobile devices.
* **Thematic Styling:** Uses Imageomics color scheme for a cohesive look and feel.
* **Longevity:** This site is run through GitHub Pages, ensuring continued access through GitHub without needing to otherwise provision dedicated infrastructure.

## Project Structure

The site runs based on four primary files:

* `public/config.yaml`: Contains all customizable settings including organization names, colors, branding, and API settings. This is the main file to edit for personalization. Placed in `public/` so Vite copies it to `dist/` without bundling, keeping it editable after deployment.
* `index.html`: The main HTML file that provides the structure of the webpage and links to the CSS and JavaScript files. Config values are applied dynamically from `config.yaml`.
* `style.css`: Custom styling for the application, including color schemes, layout, and animations. Colors are set via CSS custom properties that are populated from `config.yaml`.
* `main.js`: Handles the application's logic, including API calls, data filtering, sorting, and dynamic rendering of the catalog items.
  * **Note:** Model API calls do ***not*** return `cardData` unless explicitly fetched *by model*, so there is extra logic required to fetch Model metadata.

Two additional files support the build tooling:

* `package.json`: Declares npm dependencies (`vite`, `tailwindcss`, `@tailwindcss/vite`) and defines the `dev`, `build`, and `preview` scripts.
* `vite.config.js`: Vite configuration that registers the Tailwind CSS plugin.

### Formatting Standard

  * **What is needed:** VS Code "Format on Save" enabled with CSS & HTML format enabled.
  * **Indent Size:** 4
  * **Wrap Line Length:** 120
  * **Rules:** Remove trailing whitespace and empty tabs.

## Local Testing

This project uses [Vite](https://vite.dev/) as a build tool and requires **Node.js 24** (Active LTS). You can check your current version with `node --version`. To install or update Node, visit [nodejs.org](https://nodejs.org/en/download) or use a version manager like [nvm](https://github.com/nvm-sh/nvm):

```console
nvm install 24
nvm use
```

A `.nvmrc` file is included, so `nvm use` will automatically select the correct version in the project directory.

## Testing

Tests are written with [Vitest](https://vitest.dev/) and run automatically in CI on every pull request to `main`. To run them locally: `npm test` (single run) or `npm run test:watch` (watch mode).

`tests/validateConfig.test.js` tests the validator logic in `src/validateConfig.js`, which is also used by the `fetch-releases` and `export-tags` scripts. `tests/config.integration.test.js` confirms that the real `public/config.yaml` passes that same validation.

### Running Locally

Install dependencies and start the dev server from the repo root:

```console
npm install
npm run dev
```

Then open the local URL printed by Vite (typically <http://localhost:5173/>) in your browser of choice.

To build for production (output goes to `dist/`):

```console
npm run build
```

To preview the production build locally:

```console
npm run preview
```
