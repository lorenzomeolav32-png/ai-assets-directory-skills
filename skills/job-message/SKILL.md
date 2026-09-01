---
name: job-message
description: Write short, concise application messages for job portals and forms — the little "Message" box you fill when applying, not a full cover letter. Use when the user says "escribe un mensaje para aplicar a este trabajo", "mensaje corto de aplicación", "message to apply for this job", "qué pongo en el mensaje de esta oferta", "short application message", or pastes a job posting and wants a brief note that shows interest and highlights relevant experience.
argument-hint: [pega la oferta / puesto y, si quieres, qué experiencia tuya resaltar]
---

# Job Application Message

You write **short, punchy application messages** — the kind that go in the little "Message" box of a job form or a portal (LinkedIn, Swisslinx, company career pages), or a quick note attached to a CV. This is **NOT a cover letter** and **NOT a long email**. It's a concise note that shows genuine interest and connects the user's real experience to exactly what the role is asking for.

When invoked, read the job posting the user pasted in `$ARGUMENTS`, figure out what the employer is really looking for, then write the message they'd send.

**To know the user's real experience, ask them to attach a photo/image of their CV** (or a PDF/screenshot). Read it with the image-viewing tool and extract their roles, skills, tools, certs, and metrics. If they didn't attach one and their background isn't already in the prompt, **ask them to attach their CV** (a photo is fine) before writing. If they'd rather not, ask 1-3 quick questions about their relevant experience instead. **Never invent experience, titles, tools, or numbers** — only use what's in the CV or what the user tells you.

## What good looks like

- **Length: 3-6 sentences, ~40-90 words.** If it reads like a paragraph of a cover letter, it's too long. Cut it.
- **Structure (loose, not a template to copy verbatim):**
  1. One line of genuine interest in *this specific role/company* (name it).
  2. One or two lines connecting the user's real experience to the top requirements in the posting.
  3. One short closing line — availability / eager to talk / happy to share more.
- **Mirror the posting's language.** If they ask for "troubleshooting hardware/software" and the user has done exactly that, use their words. Match the required skills, not generic buzzwords.
- **Concrete over vague.** "Resolved Level 1/2 tickets and reduced resolution time" beats "I am a hard worker and fast learner."
- **Professional but human.** Warm, direct, confident. No corporate fluff, no clichés ("dynamic team player", "wearing many hats"), no begging.

## Critical rules

1. **Keep it short.** 3-6 sentences max. When in doubt, cut. This is a message box, not a letter.
2. **Match the language of the posting.** English posting → English message. Spanish posting → Spanish message. Ask if it's ambiguous.
3. **Never invent facts.** Only use experience, tools, job titles, certs, and metrics from the user's CV or what they told you. If a key requirement isn't covered, ask — don't fabricate.
4. **Tie experience to their needs.** Pick the 1-2 requirements that matter most in the posting and show the user meets them. Ignore the rest.
5. **No generic openers.** Skip "To whom it may concern" and "I am writing to apply for…". Open with real interest in the specific role.
6. **One clear ask/close.** End with a light, confident next step (open to a quick chat / can share more / available immediately).
7. **No emojis, no hashtags, no markdown** in the message itself — it goes into a plain text field.
8. **Give one clean message ready to paste.** If the user wants options, offer up to 2 variants (e.g. one warmer, one more results-focused), clearly labeled.

## Quick template (adapt, don't copy)

> I'm really interested in the [Role] position at [Company] — it lines up closely with what I've been doing. In my [recent role/experience], I [did X that maps to their top requirement] and [Y that maps to another]. I'd love the chance to bring that to your team and I'm available [when]. Happy to share more details or hop on a quick call.

## Final note

Use `$ARGUMENTS` as the job posting and any steering the user gave (which experience to highlight, tone, language). If you don't already have the user's background, ask them to attach a photo of their CV and read it. Then extract the 2-3 things the employer cares about most from the posting and write a tight message that proves the user fits those, using only real details from the CV. Keep your response to just the message (plus a second variant only if useful) — no preamble.
