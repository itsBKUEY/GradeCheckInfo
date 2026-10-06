# GradeCheck Privacy Policy

_Last updated: 20 September 2026_

Canonical copy: <https://github.com/itsBKUEY/GradeCheckInfo/blob/main/PRIVACY.md>

GradeCheck is a browser extension that estimates a grade for work you have already
submitted to Canvas. This policy describes exactly what it reads, what leaves your
browser, and what it does not do.

This document has not been reviewed by a lawyer. If you are publishing GradeCheck
under an organisation, or to students in a jurisdiction with its own student-data
rules, have counsel read it first.

## The short version

GradeCheck has no servers. Nothing is sent to the developers, because there is
nowhere to send it. The only outbound destination is Google's Gemini API, using an
API key you supply yourself, and the only thing sent there is the coursework being
graded together with the context needed to grade it.

## What GradeCheck reads

When you open a Canvas assignment page, GradeCheck reads the following through
Canvas's own API, using the session you are already signed in to. On a Gradescope
submission page it reads the same kinds of information from the data that page
already contains, plus your submitted code files through the request the page's own
Code tab makes. Once a Gradescope assignment is graded, it also reads your score per
question, the rubric items applied, the grader's comments and any answer key shown to
you, so it can explain the result:

- The assignment's title, description and rubric
- Your submission: the text you typed, discussion posts, and every file you uploaded.
  Documents, spreadsheets, slides, code and archives are converted to text in your
  browser. Images, audio and video recordings, and scanned PDFs are sent as files
- If you submitted a website link, the link itself (Gemini opens the page)
- The course syllabus, truncated to the first 4,000 characters
- Your previously graded work in that course: assignment names, your scores, and
  your instructor's written comments on them

That last item deserves emphasis. **Your instructor's comments about your work are
included**, because they are the best available signal for how that particular
grader behaves. They are written by another person about you.

## What is sent to Google

All of the above is assembled into a single prompt and sent to the Google Gemini API
over HTTPS, authenticated with the API key you entered on the settings page. Google
processes it under the terms attached to your own Gemini account, not under any
agreement with the GradeCheck developers.

**You should read Google's terms for the Gemini API before using this extension**,
particularly regarding whether prompts submitted on a free tier may be used to
improve their models. Free and paid tiers are treated differently. If your
coursework or your instructor's comments must not be used that way, do not use a
free-tier key.

Nothing else is transmitted anywhere. There is no analytics, no telemetry, no crash
reporting and no developer-operated backend.

Images, recordings and scanned PDFs up to about 14MB in total travel inside that
same request. Larger ones are uploaded first through Gemini's Files API, where
Google keeps them for 48 hours before deleting them automatically.

## What is stored, and where

Everything is stored locally in your browser, in `chrome.storage.local`:

- Your Gemini API key
- Estimates already produced, cached for 7 days per submission attempt
- A list of the assignments estimated, shown in the toolbar popup
- Any additional Canvas domains you have granted access to
- The on/off switch

None of this syncs to any account or leaves your device. Clearing it is immediate:
open the toolbar popup and choose **Clear**, or remove the extension.

## What GradeCheck never does

- It never writes to, edits or submits your coursework. It is read-only against Canvas.
- It never sends anything to the developers of this extension.
- It never sells, shares or brokers your data. There is no third party besides Google.
- It never reads pages other than Canvas assignment pages on domains you have permitted.
- It never collects your Canvas password. It uses the session cookie your browser
  already holds, the same way the Canvas web app does.

## Permissions, and why each is needed

| Permission | Why |
|---|---|
| `storage` | Keeps your API key, cache and settings on your device |
| `scripting` | Registers the content script on a Canvas domain you add yourself |
| `*://*.instructure.com/*`, `*://*.canvas.net/*` | Read assignment pages and call the Canvas API |
| `https://*.inscloudgate.net/*`, `https://*.canvas-user-content.com/*` | Download your uploaded submission file; Canvas serves files from these separate hosts |
| `*://*.gradescope.com/*` | Read your Gradescope submission page and its submitted files |
| `https://production-gradescope-uploads.s3-us-west-2.amazonaws.com/*` | Download the PDF you uploaded to Gradescope; it's stored on this separate host |
| `https://generativelanguage.googleapis.com/*` | Send the grading request to Gemini |
| Optional host access | Granted per domain, only when you add a school-specific Canvas address such as `canvas.school.edu` |

## Accuracy

Estimates are produced by a language model and are not grades. They carry no
authority, they are frequently wrong, and they should never be presented to an
instructor as though they came from one. The badge is deliberately styled so it
cannot be mistaken for a real score.

## Children

GradeCheck is intended for university and college students. It is not directed at
children under 13 and should not be installed for them.

## Changes

Material changes to this policy will be noted in the repository's commit history and
the date above will be updated.

## Contact

Questions and privacy requests: open an issue at
<https://github.com/itsBKUEY/GradeCheckInfo/issues>.
