---
name: film-recommendation
description: Use when the user asks for a film or movie recommendation, wants to pick what to watch next, or references reviews.md. Reads the user's film reviews and recommends movies that both satisfy their proven taste (exploit) and open new territory they haven't yet explored (explore), using gaps in their reviews to guide the exploration.
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
4. Identify the gaps: genres, languages, directors, eras, and styles that appear *nowhere* in the
   reviews. These gaps are the explore axis — the territory the user hasn't been exposed to yet.
5. Pick a recommendation and its mode.
6. Keep the answer short: one bold recommendation plus a one-line justification explaining the
   connection.

## Balancing exploit and explore

Every recommendation should either *exploit* — deliver a close match to what the user already
loved — or *explore* — open ground that is absent from their reviews. The justification should
make clear which one it is doing, and if it is exploring, name the gap it fills.

- **Three modes, all legitimate:**
  - **Mirror** — *exploit*: a close match to a top-rated film (safe, high satisfaction).
  - **Adjacent** — *explore*: shares one or two core traits (e.g. same director or theme) but
    branches into a new genre, era, or style.
  - **Stretch** — *explore*: a deliberate departure that preserves a *single* thread of their taste
    while entering genuinely unfamiliar territory (e.g. a live-action film for an animation lover,
    a foreign film, or a director they've never tried).
- **Fill the gaps.** When choosing an explore pick, prefer one that fills an obvious gap from Step 4
  (an absent genre, language, director, or era) while keeping at least one thread of their taste.
- **Narrow profiles lean explore.** When the reviews are concentrated in one cluster (e.g. all the
  same director, language, or genre), default toward explore — mirroring repeatedly only deepens the
  same narrow territory and the user stays stuck in one corner of cinema. Weigh explore picks more
  heavily until the reviews span roughly three or more distinct countries, eras, or genres.
- **Respect their dislikes, partially.** Low ratings signal avoid-this-*exactly*,
  not avoid-this-*entirely*. A disliked genre can still be recommended if the differentiator
  addresses the *why* they disliked it (e.g. they rated a slow melodrama low, but a fast-paced film
  in that genre is a fair pick).
- **Do not chase the algorithm for the user.** Never recommend purely from genre tags or "fans also
  liked" logic. Cite what makes the recommendation interesting on its own terms.
- **Balance within the request, not across answers.** There is no memory of past recommendations;
  everything is derived from `reviews.md` at request time. Balance the distance of the single pick
  against the shape of the current profile, rather than against previous answers.

## Output format

**<Title> (<Year>)** — one-sentence reason tying it to their ratings, you can also reference whether
it's a Mirror, Adjacent, or Stretch but don't use those terms because they're not widely used or
understood. The reasoning must state whether the pick mirrors what they've liked or opens new ground,

## Rules

- Never recommend a film the user has already reviewed in `reviews.md`.
- Ground every recommendation in the actual ratings; do not invent reviews.
- Keep one thread of taste in every pick, even explore ones — exploration is anchored, not random.
- If `reviews.md` is empty or missing, select a random film but one that is critically well-received
  with broad appeal and note that the recommendation is a random pick rather than based on their taste.