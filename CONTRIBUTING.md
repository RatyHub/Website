# Contributing to the Pokémon Workshop Website

Thank you for taking the time to contribute! This website is built using **Astro**, a modern framework for building fast, static-first websites, and **Markdoc**, a powerful Markdown-based content system.

Whether you want to add your own fangame, share an article, improve an existing page, or propose design upgrades, your help is highly appreciated.

---

## 🛠️ Getting Started

### Prerequisites

- **Node.js**: Version `22.12.0` or higher is required.
- **npm**: Package manager (installed automatically with Node.js).

### Setup Instructions

1. **Clone the repository:**

   ```bash
   git clone https://github.com/PokemonWorkshop/Website.git
   cd Website
   ```

2. **Install dependencies:**

   ```bash
   npm install
   ```

3. **Start the local development server:**
   ```bash
   npm run dev
   ```
   This will start the local server, usually at [http://localhost:4321/](http://localhost:4321/).
   The root URL currently shows Astro's default page, so open [http://localhost:4321/en/](http://localhost:4321/en/) or [http://localhost:4321/fr/](http://localhost:4321/fr/) to browse the website locally.

---

## ✍️ Contribution Workflows

There are two primary ways to contribute content to this website:

### 1. Creating a New Page

If you want to add a page (such as a new game page, article, tutorial, or help page):

- Create the page in the appropriate sub-directory under `src/content/pages/`.
- Name your files according to the naming convention: `<slug>_<locale>.mdoc` (where `<locale>` is either `en` or `fr`).
- **You must create files for both locales** (e.g., `my-game_en.mdoc` and `my-game_fr.mdoc`). You are welcome to use AI translations, but you **must** review them to ensure accuracy.

### 2. Improving an Existing Page

If you notice a typo, outdated information, or formatting issue:

- Locate the corresponding `.mdoc` file under `src/content/pages/`.
- Edit the content and make a Pull Request.

---

## 📁 File Structure & Naming

All page content is stored inside the `src/content/pages/` directory:

```text
src/content/pages/
├── articles/        # Articles and blog posts
├── documentation/   # Old Official SDK/Studio documentation (will be nuked)
├── games/           # Fangame presentation pages
├── help/            # Frequently asked questions and guide resources
├── learn/           # Tutorials and educational pages
└── index_en.mdoc    # Main home page (English)
```

### Naming Guidelines

- Always use lowercase and hyphens for slugs (e.g., `edelweiss-chronicles`).
- End files with `_<locale>.mdoc` (e.g., `edelweiss-chronicles_en.mdoc` and `edelweiss-chronicles_fr.mdoc`).

---

## 📝 Frontmatter Configuration

Each page starts with a YAML frontmatter block. The frontmatter properties are defined in `src/content.config.ts`. Here are the available properties:

| Key              | Type               | Required | Description                                                                                                      |
| :--------------- | :----------------- | :------: | :--------------------------------------------------------------------------------------------------------------- |
| `title`          | `string`           | **Yes**  | The title of the page (displayed as the main `<h1>` heading).                                                    |
| `seoDescription` | `string`           | **Yes**  | A short description (1-2 sentences) of the page for search engines and previews.                                 |
| `cover`          | `string[]` (paths) |    No    | An array containing the local path to the cover picture (e.g., `["./images/thumbnail.png"]`).                    |
| `tags`           | `string[]`         |    No    | Tag keys referencing definitions in `src/content/tags.json` (e.g., `wip`, `PSDK`, `PokemonStudio`, `completed`). |
| `publishDate`    | `string`           |    No    | Publication date of the page, formatted as `'YYYY-MM-DD HH:MM:SS'`.                                              |
| `order`          | `number`           |    No    | Number used to sort pages in lists/index layouts (higher numbers appear later or custom order).                  |

### Frontmatter Example

```yaml
---
title: Pokémon Stalactite
seoDescription: Dive into the heart of a frozen epic in Pokémon Stalactite. Will you uncover the Citados region secrets?
cover:
  - './images/pokemon-stalactite-thumbnail.png'
tags:
  - wip
  - PSDK
  - PokemonStudio
publishDate: '2026-04-23 15:31:00'
order: 20260423
---
```

---

## 🖼️ Media & Images

To ensure clean and organized assets:

1. **Store images locally:** Put your image files in an `images` subfolder within the directory containing your `.mdoc` page.
   - For a game page: `src/content/pages/games/images/`
   - For an article page: `src/content/pages/articles/images/`
2. **Reference images:** Use local relative paths in markdown image syntax:
   ```markdown
   ![Description of the screenshot](./images/my-screenshot.png)
   ```
3. **Figure Captions:** To add a caption under your image, use a `¤` character to separate the image alt text and the caption:
   ```markdown
   ![Blue Artwork¤Blue](./images/image_2022-08-20_223107780.png)
   ```
   This will render the image with `alt="Blue Artwork"` and a caption (using the `<figcaption>` element) showing `Blue`.

---

## 🧩 Markdoc Custom Tags

We extend standard Markdown with Markdoc tags to build complex page layouts. Use the following custom tags to format your content:

### 1. Row & Columns (`{% row %}` & `{% column %}`)

Organizes content into multi-column layouts (ideal for listing credits, starters, or side-by-side elements).

- **`{% row %}` Attributes:**
  - `columns` (**required**): Defines the column layout. Allowed values:
    - `'1/1'`, `'1/2'`, `'1/3 1/3 1/3'`, `'1/3 2/3'`, `'2/3 1/3'`, `'1/4 1/4 1/4 1/4'`, `'1/4 3/4'`, `'3/4 1/4'`
  - `bottom_margin` (optional): Vertical space below the row. Matches: `'margin-s'`, `'margin-m'`, `'margin-l'`, `'margin-xl'`, `'margin-xxl'`. (Defaults to `'margin-m'`).
  - `centered_content` (boolean, optional): Align column content vertically centered.
  - `centered_items` (boolean, optional): Center items horizontally.
  - `centered_text` (boolean, optional): Center text horizontally.
  - `last_to_bottom` (boolean, optional): Align the last item in a column to the bottom.

- **Usage Example:**

  ```markdown
  {% row columns="1/3 1/3 1/3" bottom_margin="margin-m" centered_text=true %}
  {% column %}

  ### Creature1

  ![Artwork of Creature1](./images/creature1.png)
  {% /column %}

  {% column %}

  ### Creature2

  ![Artwork of Creature2](./images/creature2.png)
  {% /column %}

  {% column %}

  ### Creature3

  ![Artwork of Creature3](./images/creature3.png)
  {% /column %}
  {% /row %}
  ```

---

### 2. Call To Action (`{% cta %}`)

Renders a styled action button.

- **Attributes:**
  - `href` (optional): The URL destination.
  - `align` (optional): Button alignment. Allowed values: `'left'`, `'right'`, `'center'`.

- **Usage Example:**
  ```markdown
  {% cta href="https://discord.gg/your-invite" align="center" %}Join Discord{% /cta %}
  ```

---

### 3. Page Reference Card (`{% pageRef %}`)

Renders a visual card that previews another page of the website.

- **Attributes:**
  - `id` (**required**): Path to the target page relative to `src/content/pages/` excluding the `.mdoc` extension (e.g., `games/foret-eternelle_en`).
  - `description` (optional): Custom text description to show on the card. Set to `"source"` to automatically use the target page's `seoDescription`.

- **Usage Example:**
  ```markdown
  {% pageRef id="games/pokemon-blank_en" description="source" /%}
  ```

---

### 4. Index Listing (`{% index /%}`)

A self-closing tag used as a placeholder in main list pages (such as `/games/index_en.mdoc`) to automatically generate a grid of links to all sub-pages under the category.

- **Usage Example:**
  ```markdown
  {% index / %}
  ```

---

## 🔍 Local Verification & Testing

Before proposing your changes, verify that your pages build and look correct:

1. Start your local dev server: `npm run dev`
2. Navigate to your page in a web browser using the format:
   `http://localhost:4321/<locale>/<path_to_page>/<slug>`
   - **Example:** `http://localhost:4321/en/games/pokemon-stalactite/`
   - **Example:** `http://localhost:4321/fr/articles/pokemon-studio-open-source/`
3. Check the layout, check that cover images load, make sure text is formatted properly, and links work.

---

## 🎨 Design & Code Improvements

We welcome code and style updates to improve the website's performance, layout, typography, or styling!

- Code styles are formatted using **Prettier**. You can format your files automatically before committing:
  ```bash
  npx prettier --write .
  ```
- Ensure pages look good and scale correctly across all screen sizes (responsive design).

---

## 🚀 Submitting Your Changes

1. Push your changes to your own fork of the project.
2. Go to the [Pokémon Workshop Website Pull Requests](https://github.com/PokemonWorkshop/Website/pulls) page.
3. Open a new Pull Request comparing your fork and branch to the `main` branch of `PokemonWorkshop/Website`.
4. Provide a clear description of what has changed or what new page has been added!
