# Property Mini-Listings 🏡

A small Vue 3 single-page app built for **Module 1 – Exercise 03** (Life Choices Academy).
It shows a fictional Cape Town short-term rental brand, "Homes & Beyond", with a
card-based listings page that can be searched and sorted by price.

## Overview

- Listings are stored locally in `src/App.vue` (no backend or API calls).
- Users can search by **title or location**.
- Users can **sort by price** (low → high / high → low) with one button.
- Unavailable properties show a red "Not Available" ribbon and a disabled
  "Enquire Now" button.
- Each card can be **bookmarked** (heart icon) — the saved count updates in the header.
- The header shows the brand name and live counts: total listings, active listings,
  and saved listings.

## Tech used

- Vue 3 (Composition-free, Options API) + Vite
- Plain JavaScript (no TypeScript)
- No router, no external UI libraries

## Project structure

```
src/
  components/
    AppHeader.vue     -> brand + stats (props only)
    FilterBar.vue      -> search input + sort button
    PropertyCard.vue   -> single listing card (props + emits)
  App.vue               -> holds the data array, search/sort/bookmark logic
  main.js
  assets/main.css
```

## Installation & running locally

1. Make sure you have **Node.js** installed (v16+ recommended).
2. Clone this repository and move into the folder:
   ```bash
   git clone https://github.com/totoseahlumile-dot/property-mini-listings.git
   cd property-mini-listings
   ```
3. Install dependencies:
   ```bash
   npm install
   ```
4. Start the dev server:
   ```bash
   npm run dev
   ```
5. Open the URL shown in the terminal 

## Screenshot

> 
>
> <img width="1618" height="856" alt="image" src="https://github.com/user-attachments/assets/8702090c-f2f8-4983-921b-191bf0a41fe9" />


## Notes / things I'd improve with more time

- Persist bookmarks in `localStorage` so they survive a page refresh (stretch goal).
- Add a price range slider filter.
- Add small transitions when cards re-sort/filter.

## Submission

- Repository name: `property-mini-listings`
  
