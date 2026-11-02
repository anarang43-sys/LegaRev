# LegaRev.AI

LegaRev.AI is a static blog that reviews AI models on Indian corporate and
transactional legal work. It is built with Jekyll and runs on GitHub Pages
with no build step of your own: no npm, no framework, nothing to install.
GitHub builds it for you every time you push.

This README explains, in plain English, how to add a new review and how to
update the scorecard. You do not need to know Jekyll to do either.

## How the site is organised

- `_reviews/`: one Markdown file per review. This is the "reviews
  collection".
- `_data/scorecard.yml`: the one file behind the scorecard table.
- `_layouts/`, `_includes/`, `assets/`: the templates and the stylesheet.
  You should not normally need to touch these.
- `index.html`, `reviews/index.html`, `scorecard.html`, `methodology.html`,
  `about.html`, `disclosures.html`, `contact.html`: the site's pages.

## Adding a new review

1. In `_reviews/`, copy the sample file `2026-01-15-sample-model-a.md` and
   rename the copy, for example `2026-03-01-claude-opus-5.md`. The date at
   the start of the filename should match the date you tested the model.

2. Open the new file and fill in the front matter (the block between the
   `---` lines at the top):

   - `title`: the name shown as the page title, usually the model name.
   - `review_no`: the next number in sequence (check the existing
     reviews to find the last one used).
   - `model`: the model's name, e.g. `GPT-5.1`.
   - `version`: the version or date stamp of the model you tested.
   - `tested_on`: the date you ran the test, as `YYYY-MM-DD`.
   - `date`: same date, used to sort and display the review (no quotes).
   - `access`: how you accessed the model, e.g. `Public API, default settings`.
   - `overall`: the overall mark out of 10, e.g. `7.8`.
   - `scores`: the five marks out of 10, which are `accuracy`, `reasoning`,
     `hallucination`, `drafting` and `instructions`.
   - `headnote`: a short paragraph summing up the review, like a case
     headnote.
   - `held`: the verdict, in a sentence or two, like a court's "held".
   - `strengths` / `weaknesses`: short bullet lists.
   - `questions`: one entry per question in the test paper, each with
     `num` (the question number), `prompt` (the question asked), `answer`
     (the extract of the model's actual answer, pasted in) and `note`
     (your note as the marker).

3. Delete the `sample: true` line. That line is what marks a review as a
   placeholder. Leaving it out means the review shows up as real.

4. **Never invent a score.** If you have not tested a question, or a
   category, yet, write `TBC` instead of a number. `TBC` is also what the
   sample review uses throughout, so you can see what an untested score
   looks like.

5. Save, commit and push. GitHub Pages rebuilds the site automatically.
   The new review appears on the Reviews page and, if it is one of the
   three most recent, on the homepage.

## Updating the scorecard

The scorecard is one file: `_data/scorecard.yml`. It is a simple list,
one entry per model. To add a model, copy one of the sample entries and
fill in:

- `model`, `version`: same as in the review.
- `agreement_review`, `drafting`, `regulatory`, `issue_spotting`,
  `citations`: the five scorecard categories, out of 10 (or `TBC`).
- `overall`: the overall mark. The table sorts on this field automatically,
  highest first, so you do not need to reorder anything by hand.
- `review_url`: the path to the full review, e.g.
  `/reviews/2026-03-01-claude-opus-5/` (this matches the review file's
  name, without the `.md`).

Do not include the `sample: true` line for a real entry. That line is
only there to mark the two placeholder rows so readers can tell they are
not real results. Once you have added your first real scorecard rows, you
can delete the two sample rows from this file.

## The newsletter button

The Subscribe button in the header and the dark band on the homepage both
link to `newsletter_url` in `_config.yml`. It is currently a placeholder
(`#`). Replace it with wherever you end up running the newsletter (for
example a Buttondown, Substack or Mailchimp signup page). This site does
not collect email addresses itself.

## Running it locally (optional)

You do not need this to publish. GitHub Pages builds the site for you.
If you want to preview changes on your own machine first, you need Ruby
and Jekyll installed, then from the repository root:

```bash
gem install bundler jekyll
jekyll serve
```

This serves the site at `http://localhost:4000`.
