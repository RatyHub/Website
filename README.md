# Pokémon Workshop Website

This repository contains the source code for the official [Pokémon Workshop](https://pokemonworkshop.com/) website. The site is built with [Astro](https://astro.build/), a modern static site generator / web framework.

## 🚀 Migration from KirbyCMS to Astro

Previously, the Pokémon Workshop website was powered by KirbyCMS. We decided to migrate to Astro due to the end of support for Kirby 3. 

Leaving an unsupported CMS on our server would have exposed us to potential security vulnerabilities. Upgrading to a supported version (Kirby 5) would have required purchasing a new license and dealing with complex, extensive breaking changes between Kirby 3 and Kirby 5. Ultimately, maintaining a dynamic CMS did not grant better security compared to a static HTML website.

By moving to Astro, we generate a fully static site that:
- Eliminates server-side execution security risks.
- Provides superior loading speeds and performance.
- Simplifies our hosting infrastructure.

## ✍️ Adding my project page or improve a page

If you want to add your project page, correct an error, or improve any part of the website, we would love your help! Please refer to our [CONTRIBUTING.md](/CONTRIBUTING.md) guide for instructions on how to submit changes.

## 🧞 Commands

All commands are run from the root of the project, from a terminal:

| Command                   | Action                                           |
| :------------------------ | :----------------------------------------------- |
| `npm install`             | Installs dependencies                            |
| `npm run dev`             | Starts local dev server at `localhost:4321`      |
| `npm run build`           | Build your production site to `./dist/`          |
| `npm run preview`         | Preview your build locally, before deploying     |
| `npm run astro ...`       | Run CLI commands like `astro add`, `astro check` |
| `npm run astro -- --help` | Get help using the Astro CLI                     |

## 👀 Learn More

To learn more about Astro, check out the [Astro Documentation](https://docs.astro.build/).
