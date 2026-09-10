# Contributing to Pausch Lab Roadmap

This is a **curated lab curriculum**, not a general link directory. It is maintained by Pausch Lab @ [Next Tech Lab](https://ntlap.in/) and serves as the primary learning path for lab associates. External contributions are welcome when they meet the bar below — quality over quantity.

---

## 1. What We Accept

We accept contributions that make someone **learn better**, not just collect more links.

**Accepted:**
- Fixing outdated APIs, deprecated packages, or version drift (e.g., Unity 6.3 LTS migration, OpenXR 1.1, Horizon OS v205)
- Replacing a weak resource with a stronger, actively maintained one with a clear reason
- Adding a missing skill, exercise, or milestone that was tested on device
- Correcting technical inaccuracies, typos, or broken links

**Not accepted:**
- Bulk link dumps or "add my tutorial / my repo" without justification
- Resources targeting deprecated versions (Unity 2021/2022 legacy pipelines, old XR SDKs, pre-OpenXR flows)
- AI-generated summaries, filler content, or untested copy-paste code
- Self-promotion without pedagogical value

If in doubt, open an issue first and propose the change before writing a PR.

---

## 2. Quality Bar

Every change must be:

1.  **Version-accurate** — Target the current stable: Unity 6.3 LTS (support to Dec 2027), UE 5.6, Godot 4.5, Horizon OS (Meta XR SDK v205.0, Quest 3/3S), visionOS 26, WebGPU Baseline 2026 / OpenXR 1.1. State the version you verified against.
2.  **Tested or verified** — You ran the sample, built to device, or checked the docs. Do not submit what you have not verified.
3.  **Pedagogical** — Explain *what skill* the resource teaches, not just what it is. Prefer docs and production-tested guides over shallow videos.
4.  **Concise and technical** — No slang, filler, emojis, or marketing language. Tables over long bullet lists when comparing options.

---

## 3. How to Contribute

### Step 1 — Propose (for non-trivial changes)

Open an issue with:

- What you want to change and why
- Which section/track it affects and which version it targets
- Link to the proposed resource or fix

Lab maintainers will confirm scope before you invest time. Pausch Lab associates may skip this for small fixes.

### Step 2 — Make the Change

1. Fork the repository.
2. Create a focused branch:

   ```bash
   git checkout -b docs/update-unity-xri-6-3
   # or: fix/quest-pca-resolution-note, chore/typo-xr-foundations
   ```

3. Keep the PR scoped to **one track or one topic**. Do not bundle unrelated changes.
4. Follow the style guide in Section 4.
5. Verify all links resolve and versions are correct.

### Step 3 — Commit

Use clear commit messages:

```bash
git commit -m "docs(xr): update Passthrough Camera API to Horizon OS v83 (1280x1280)"
git commit -m "docs(gamedev): replace deprecated URP 2022 reference with Render Graph (Unity 6.3)"
git commit -m "fix: correct OpenXR reference space description"
```

### Step 4 — Pull Request

Open a PR against `main` and fill in:

- **Summary:** What changed.
- **Reason:** Why it improves learning (skill gained, deprecated API removed, accuracy fixed).
- **Verification:** How you verified — docs link, device tested, build URL, or emulator check.
- **Version:** Engine/SDK/OS version the change was checked against.

Example:

> **Summary:** Replaced XRI 2.x sample with XRI 3.x + Interaction SDK ThrowTuner note.
> **Reason:** Old sample uses deprecated affordance system; new path is the production standard for Quest 3/3S.
> **Verification:** Built on Quest 3S, Horizon OS v83, Unity 6.3 LTS — stable 90 Hz, docs: developers.meta.com/.../unity-isdk-setup
> **Version:** Unity 6.3 LTS / Meta XR SDK v205.0

---

## 4. Style Guide

- **Headings:** Sentence case. One `#` for file title, `##` for sections.
- **Tone:** Technical, direct, concise. No "dive into", "unlock", "supercharge", or similar filler.
- **Formatting:** Use tables to compare options (SDKs, frameworks, specs). One-line resource format: `[Title](URL) — What skill it teaches.`
- **Links:** Must resolve, must be canonical (prefer `developers.meta.com`, `docs.unity3d.com`, `developer.apple.com` over aggregators). Check before submitting.
- **Dates:** When citing platform state, include verification date, e.g., `Last verified: September 2026`.

---

## 5. Review Process

- All PRs are reviewed by **Pausch Lab maintainers**. This is an editorial curriculum — not every PR is merged.
- Expect feedback on accuracy, pedagogy, and fit. Small, well-evidenced PRs are merged fastest.
- Large or opinionated changes (new track, new milestone) require an approved issue first.
- Do not bump PRs within 48 hours. Lab review runs on the lab's schedule.

---

## 6. Quick Checklist Before Submitting

- [ ] Change is scoped to one topic
- [ ] Versions are current and stated in the PR
- [ ] Links are live and canonical
- [ ] Tone is concise, no AI filler or slang
- [ ] You have verified the change (docs or device)
- [ ] PR description explains *why* — not just *what*

---

*Questions? Open an issue. For lab associates, reach out on the Pausch Lab channel before contributing externally.*

*Maintained by Pausch Lab @ [Next Tech Lab](https://ntlap.in/).*
