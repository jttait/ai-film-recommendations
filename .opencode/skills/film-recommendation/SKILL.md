---
name: film-recommendation
description: Use when the user asks for a film or movie recommendation, wants to pick what to watch next, or references reviews.md. Reads the user's film reviews and recommends movies matched to their taste, mixing similar and divergent picks so their viewing stays varied.
---

# Film Recommendation

Recommend a film to watch based on the user's personal reviews stored in `reviews.md`.

## When to use

Use whenever the user asks for a film/movie to watch, a recommendation, or says "recommend a film".
Trigger keywords: *recommend*, *what should I watch*, *movie*, *film*, *reviews.md*.

## Steps

1. Read `reviews.md` at the project root.
2. Parse each entry (format: `Title (Year) ⭐s`). Note the title, year, and star rating for each
   film.
3. Build the user's taste profile from the highest-rated films (4-5 stars). Consider genre,
   director, studio, animation style, themes, and era. Low-rated films signal what to avoid.
4. Pick a recommendation and its mode.
5. Keep the answer short: one bold recommendation plus a one-line justification explaining the
   connection.

## Keeping recommendations varied

The goal is a *mix*, not the loudest single answer every time. Whatever the state of the profile,
the failure mode to avoid is every recommendation mirroring the same small cluster of taste, so the
user would only ever watch similar films.

- **Three modes, all legitimate:**
  - **Mirror** — a close match to a top-rated film (safe, high satisfaction).
  - **Adjacent** — shares one or two core traits (e.g. same director or theme) but branches into a
    new genre, era, or style.
  - **Stretch** — a deliberate departure that preserves a *single* thread of their taste while
    exploring unfamiliar territory (e.g. a live-action film for an animation lover, a foreign film,
    or a director they've never tried).
- **Mix across recommendations.** Aim for roughly balanced coverage across modes over successive
  recommendations, not one mode every time. `Mirror` is often what the user wants and is fine to
  give — just avoid repeating it back-to-back when the signal points somewhere reflective.
- **Vary the axis.** If the last recommendation matched by *director*, this time match by *theme* or
  *mood* instead. Do not chain recommendations along the same similarity axis.
- **Respect their dislikes, partially.** Low ratings signal avoid-this-*exactly*,
  not avoid-this-*entirely*. A disliked genre can still be recommended if the differentiator
  addresses the *why* they disliked it (e.g. they rated a slow melodrama low, but a fast-paced film
  in that genre is a fair pick).
- **Do not chase the algorithm for the user.** Never recommend purely from genre tags or "fans also
  liked" logic. Cite what makes the recommendation interesting on its own terms.

## Output format

**<Title> (<Year>)** — one-sentence reason tying it to their ratings, you can also reference whether
it's a Mirror, Adjacent, or Streth but don't use those terms because they're not widely used or
understood.

## Rules

- Never recommend a film the user has already reviewed in `reviews.md`.
- Track which modes and axes were used in recent recommendations; keep the mix varied rather than
  repeating the same mode.
- Ground every recommendation in the actual ratings; do not invent reviews.
- If `reviews.md` is empty or missing, select a random film but one that is critically well-received
  with broad appeal and note that the recommendation is a random pick rather than based on their taste.
