# Colostrum6 Compliance Checker

A self-check tool for Anovite Independent Associates to screen draft social media posts, captions, and messages against the **Anovite Compliance Quick-Reference Guide** before submitting them for official approval.

**This is a self-check tool only.** It does not replace, and is not a substitute for, written approval from Anovite Compliance. Per the Quick-Reference Guide (§9): do not publish, post, print, or distribute any content until written approval is received from `anovitecompliance@gmail.com`.

---

## What it does

- **Check Content tab** — paste a draft post/caption/message and run a check. The tool scans the text against a fixed rule set drawn directly from the Quick-Reference Guide and flags:
  - Named diseases/conditions that should never be mentioned (§2.3)
  - Prohibited drug-claim verbs like "cure," "treat," "diagnose" (§2.1)
  - Substitute-for-therapy language (e.g. comparing the product to medication or HGH injections) (§1.3)
  - Claims that the product augments or counteracts a drug/medical therapy (§1.2)
  - Antimicrobial/pathogen-fighting language (§1.3)
  - Testimonial health claims ("cured my...", "healed my...") (§3)
  - Personal income claims (§4)
  - Missing FDA disclaimer (§7)
  - Missing "[Name], Anovite Independent Associate" identification (§5.1)

  Each flag comes with a plain-English explanation, the specific guide section it's based on, and a suggested compliant rewrite.

- **Product Facts Reference tab** — neutral, non-claim facts about Colostrum6 (sourcing, dosage mechanics, certifications, pricing) associates can reference. These are explicitly **not** pre-approved marketing language.

- **My History tab** — a running log of past checks, saved locally in your browser only.

## What it is NOT

- **Not an AI tool.** There is no language model involved. Every check is deterministic pattern-matching against a fixed rule set — the same input always produces the same result.
- **Not a replacement for human compliance review.** It reliably catches named diseases, banned verbs, and known risky phrases. It will **not** catch a cleverly-worded implied claim that avoids all flagged words (e.g., describing symptoms improving without naming the condition). That kind of judgment call still needs a person.
- **Not connected to anything.** No network calls, no accounts, no data sent anywhere. Everything runs entirely in your browser.

## How to use it

1. Open the tool (see **Deployment** below for how it's hosted).
2. Paste your draft content into the **Draft Content** box.
3. Click **Run Compliance Check**.
4. Review the verdict:
   - **Looks Compliant** — no issues found against the rules checked here. Still send it to `anovitecompliance@gmail.com` for written approval.
   - **Add Disclaimer & ID** — your claim language is fine, but the required FDA disclaimer and/or associate identification is missing. Add them, then it's ready to submit.
   - **Needs A Look** — one or more items need a second look before this is ready.
   - **Revise Before Sending** — one or more likely violations were found. Revise using the suggested rewrites before submitting.
5. Once you're happy with the draft, send it to `anovitecompliance@gmail.com` as usual. The tool does not submit anything on your behalf.

## Deployment

This is a single self-contained HTML file (`compliance-checker.html`) — no server, database, or build step required.

**Recommended: GitHub Pages**
1. Create a free GitHub Organization (keeps this separate from any personal GitHub account).
2. Create a public repository inside that organization and upload `compliance-checker.html`.
3. In the repo, go to Settings → Pages → set Source to "Deploy from a branch" (`main`, `/ root`).
4. GitHub will publish a live URL — share that link with your downline.

**Alternatives:**
- Host it on any other static file host (Google Sites, a shared Drive link, your own website, etc.).
- Email the `.html` file directly — anyone can open it locally in a browser with no setup.

No matter how it's hosted, the tool always works the same way, since it runs entirely client-side.

## Updating the rule set

The rules live near the top of the `<script>` section in `compliance-checker.html`, as plain JavaScript arrays and regular expressions:

| Constant | Purpose |
|---|---|
| `NEVER_MENTION` | Named diseases/conditions that can never be mentioned |
| `HARD_BANNED_VERBS` | Verbs that are (almost) always a violation |
| `CONTEXT_VERBS` | Verbs that are only a violation in certain contexts (flagged as a caution) |
| `VERB_REPLACEMENTS` | Suggested compliant replacement for each banned/context verb |
| `SUBSTITUTE_DRUG_PATTERNS` | Phrases positioning the product as a drug/therapy substitute |
| `AUGMENT_DRUG_PATTERNS` | Phrases claiming the product augments/counteracts a therapy |
| `ANTIMICROBIAL_PATTERNS` | Antimicrobial/pathogen-fighting language |
| `TESTIMONIAL_HEALTH_PATTERNS` | Testimonial phrases like "cured my..." |
| `INCOME_CLAIM_PATTERNS` | Dollar-figure income claims |

To add a new flagged term or phrase, add it to the relevant array/pattern list. No other code changes are needed — the results UI and history log will pick it up automatically.

If Anovite updates the Quick-Reference Guide, these rule lists should be reviewed against the new version to keep them accurate.

## Source

Rules are drawn from the *Anovite Compliance Quick-Reference Guide* (based on Anovite Policies and Procedures, FDA 21 CFR §101.93, and related Anovite compliance materials). Product facts are drawn from Anovite's Colostrum6 product information sheets, limited to neutral, non-claim facts only.
