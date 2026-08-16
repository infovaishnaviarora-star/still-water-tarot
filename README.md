# Still Water Tarot

A single-page site for a tarot reading practice — hand-read oceanic tarot.

Everything is in `index.html`: markup, styles, scripts, fonts and imagery are all
inlined, so the site is one self-contained file with no build step and no external
requests.

## What's inside

- **Hero card arc** — seven cards ride a wide circle and step one slot at a time
  (0.55s eased slide, 1s rest). Drag or swipe horizontally to spin it; vertical
  swipes are left to the page so scrolling always works.
- **Scroll-scrubbed background** — a 52-frame watercolour sequence drawn to a fixed
  canvas and scrubbed by scroll position. Phones decode every third frame to keep
  memory down, and the loop idles when the arc is off-screen.
- **Contact form** — client-side validation, then a POST to a form service.
  See "Form delivery" below.
- **Responsive** — a dedicated phone scale below 560px: 32px headings, 16px body,
  16px form fields (below that iOS zooms on focus), and an 18px gutter throughout.

## Form delivery

Submissions POST to [FormSubmit](https://formsubmit.co), configured at the top of
the contact-form script in `index.html`:

    const ENDPOINT = 'https://formsubmit.co/ajax/<address>';

FormSubmit needs no account. The first message sent to a new address triggers a
one-off confirmation email; delivery starts once that link is clicked.

Once activated, FormSubmit issues a random alias for the same inbox. Swapping the
address in `ENDPOINT` for that alias keeps it out of the page source, away from
scrapers.

The thank-you panel appears only when the service confirms it took the message.
A failed send leaves the form filled in and says so.

## Local preview

    python3 -m http.server 8000

then open http://localhost:8000

## Deployment

Served as a static file by GitHub Pages from the default branch.
