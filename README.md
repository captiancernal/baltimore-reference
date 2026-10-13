# Baltimore Reference

A Baseball-Reference-style site for an MLB The Show Orioles dynasty: season pages, player cards, comparisons, leaderboards, analytics, projections, a franchise timeline, the Orioles Hall of Fame, and daily trivia.

The site reads the **MLB The Show Dynasty Database** Google Sheet live. Add a season to the sheet and the site picks it up on the next page load. There's no build step and no data file to update.

## Setup

### 1. Make the sheet viewable

The site reads the sheet the same way a visitor would, so it needs view access.

1. Open the **MLB The Show Dynasty Database** sheet.
2. Click **Share**.
3. Under **General access**, choose **Anyone with the link**, with the role **Viewer**.

Anyone with the link can view the sheet. Nobody but you can edit it.

### 2. Publish with GitHub Pages

1. Create a repository, for example `baltimore-reference`.
2. Upload `index.html` and `og-image.png` to the root of the repo.
3. Go to **Settings → Pages**.
4. Under **Build and deployment**, choose **Deploy from a branch**, then select `main` and `/ (root)`.
5. After a minute or two, the site is live at `https://YOUR-USERNAME.github.io/baltimore-reference/`.

### 3. Turn on link previews

Group chats and Discord need the full address of the preview image. In `index.html`, replace `og-image.png` on these two lines with the image's full URL:

```html
<meta property="og:image" content="https://YOUR-USERNAME.github.io/baltimore-reference/og-image.png">
<meta name="twitter:image" content="https://YOUR-USERNAME.github.io/baltimore-reference/og-image.png">
```

## Updating

Keep adding seasons to the Google Sheet exactly as before. Visitors see the new data the next time they open the site, and the **Refresh data** button in the footer reloads it right away.

The site finds each column by its header name. If you add new columns, nothing breaks. If you rename a column, it may stop showing on the site.

## Troubleshooting

- **"Can't read the dynasty sheet."** The sheet's sharing isn't set to *Anyone with the link: Viewer*. Change it and reload.
- **A value is missing on the site but present in the sheet.** Google's export guesses each column's type. If a column mixes numbers and text (for example, a number column with a word typed in it), Google may blank the odd ones out. Keep each column to one kind of value.

## What's in it

- **Home:** a pennant wall of every season, franchise totals, and leaderboards.
- **Seasons:** standings, team stats, batting and pitching tables, the playoff bracket, award finalists, the 99 Club, and roster changes.
- **Players:**
  - Searchable list.
  - Player cards: year-by-year tables, rating-by-age charts, accolades, teammates, similar Orioles, a next-season projection, and a downloadable card image.
- **Compare:** up to four players side by side, with charts.
- **Leaders:** single-season and career boards.
- **Analytics:** roster strength, aging curves, continuity, talent vs. wins, and more.
- **Projections:** next season's ratings, based on how Orioles at each age have changed year to year.
- **Timeline:** every season's wrap-up, with titles, awards, and records.
- **League:** award winners, World Series history, team pages, and former Orioles elsewhere.
- **Hall of Fame:** plaques with career lines.
- **Trivia:**
  - Daily challenge: the same 10 questions for everyone, a shareable result, and a streak counter.
  - Practice rounds, as many as you like.
- **Glossary:** every stat explained.

Trivia scores, streaks, and the light/dark setting are saved in each visitor's own browser.
