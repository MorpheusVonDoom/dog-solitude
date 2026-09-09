---
name: update-page
description: 'Update one or more pages on the Mona Lisa Overdrive MkDocs website. Use when editing the homepage, show dates, photos, videos, about, EPK, press, or navigation content in the docs folder.'
argument-hint: '<page-name-or-section> <short-summary>'
user-invocable: true
disable-model-invocation: false
---

# Update Page Skill

This skill helps maintain the Mona Lisa Overdrive MkDocs website by updating source pages in the docs folder and, when needed, keeping the nav and metadata in the MkDocs configuration aligned.

## Workspace Map

- Source content lives in `mlo-website/docs/`
- Site configuration lives in `mlo-website/mkdocs.yml`
- Generated static HTML goes in `mlo-website/site/` and should not be hand-edited

## When to Use

Use this skill for tasks such as:

- Updating the homepage: `docs/index.md`
- Updating show-date content: `docs/show-dates.md`
- Updating band/about content: `docs/about.md`
- Updating photo gallery content: `docs/photos.md`
- Updating video page content: `docs/videos.md`
- Updating EPK and press pages: `docs/epk.md` and `docs/press.md`
- Changing or adding links inside the MkDocs navigation in `mkdocs.yml`

## Procedure

1. Decide which page or pages are the real source of truth in `mlo-website/docs/`.
2. Inspect the existing file format first and treat the current page structure as the template for the requested change. Use the markup pattern as the only model; do not copy content values from previous entries.
3. Ask the user for any missing details needed to make the update match the existing format. Ask only for the values, links, or files required by the template, such as title, date, venue, address, location, image path, video URL, music link, card copy, and other event fields.
4. For the show-dates page, preserve the event-card HTML structure that exists in the file: `event-card`, `data-date`, `event-date`, `event-venue`, `support-acts`, `ticket-price`, `ticket-link`, `age`, `show-time`, `event-details`, and optional embedded Google map `iframe` and show-cta links. Keep the same order and nesting as the format shows.
5. If a show card is created for an upcoming event, keep it in the `Upcoming Shows` section of `mlo-website/docs/show-dates.md`. If the `data-date` has passed, move that event into the `Past Shows` section in the same file as a `<details>` block. Do not delete or overwrite the prior event cards already in the same page.
6. If the page already exists, edit that markdown file directly using the same structure, headings, card layout, ordering, captions, and link style already present.
7. If the page is new, add or rename the correct entry in `mlo-website/mkdocs.yml` nav.
8. For any update type — text, image, gallery card, new video, music item, external link, social link, or event card — follow the same rule: identify the target file, inspect the current format, ask for any missing values, links, or files, and add the new material in the same shape as the existing format.
9. Keep all image, gallery, and media references relative to the docs folder and use the same file naming conventions already used by the site.
10. For event cards that include a venue address or location detail, list the address in the `event-details` text and, when supported, embed a Google map `iframe` with the same address in the event card. Ask for the address and map URL or file when they are not already provided by the user.
11. Do not edit generated files in `mlo-website/site/`.
12. Build the site from the `mlo-website/` folder with `mkdocs build --clean` or preview with `mkdocs serve`.
13. If the page content appears in multiple places, keep the pages consistent with the same tone, page titles, and social links.

## Content Rules

- Prefer editing the markdown source in the docs folder instead of rewriting rendered HTML.
- Keep navigation changes in `mkdocs.yml` and page content changes in the matching `.md` file.
- Preserve the existing Material theme and custom CSS hooks.
- Match page headings, image captions, show/date cards, photo cards, videos, music entries, and link blocks to the current site style.
- Always match the existing format and use it as the template for any new material or update.
- For any requested update, gather missing details from the user before producing the new content block, image entry, link, card, or media item. Ask directly for the missing values, URLs, or uploaded files; do not fill them from a previous item in the repo.
- For show-date cards and related event entries, keep the original card structure intact and add missing event fields such as address text and map iframe in the same markup style already used by the repo. Do not echo or infer values from earlier show entries; only use the format as the scaffold and fill in fields from the new request.
- Never delete older event cards from the same source page when adding or moving a new card. Preserve all prior entries and only relocate passed cards from `Upcoming Shows` to `Past Shows` by section.

## Verification

After making page updates:

- confirm the destination markdown file is in `mlo-website/docs/`
- confirm `mlo-website/mkdocs.yml` reflects any newly named or moved pages
- verify that the inserted material follows the same existing formatting pattern as nearby entries
- run a local MkDocs build from `mlo-website/` to ensure the update compiles cleanly
