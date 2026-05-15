# Contributor Acceptance Automation + Certificate Workflow

This repository is a reusable GitHub Actions setup for programs like **Evangelists** (or any contributor program) where:

1. A candidate opens a PR to add their details.
2. A welcome/review workflow posts follow-up questions and tags reviewers.
3. After the PR is merged, an acceptance email is sent automatically.
4. A certificate is generated and attached to that email.

It is inspired by the AOSSIE Evangelists process:
https://github.com/AOSSIE-Org/Info/blob/main/Roles/Evangelists.md

---

## Workflows included

### 1) `.github/workflows/evangelist-welcome.yml`
- Trigger: `pull_request_target` on PR open
- Path filter: `Evangelists.md`
- Actions:
  - Posts onboarding questions on the PR
  - Mentions reviewers from `.github/evangelist-reviewer`
  - Adds label `evangelist-application`
  - Assigns the PR author

### 2) `.github/workflows/evangelist-acceptance-email.yml`
- Trigger:
  - PR closed (runs only if merged + `evangelist-application` label is present), or
  - Manual `workflow_dispatch` for testing
- Actions:
  - Parses applicant details
  - Generates certificate via `.github/scripts/generate_certificate.py`
  - Sends acceptance email with certificate attachment

---

## Quick setup

1. Clone this repository.
2. Rename terms for your organization/program:
   - Replace `AOSSIE` with your org name.
   - Replace `Evangelists` with your program name.
   - Replace `.github/evangelist-reviewer` entries with your reviewer usernames.
3. Configure repository secrets:
   - `AOSSIE_MAIL_USERNAME`
   - `AOSSIE_MAIL_PASSWORD`
   - `AOSSIE_ADMIN_BCC_EMAIL` (optional but recommended)
4. Ensure applicants include an email in their PR body (required by acceptance mail workflow).
5. Test via `workflow_dispatch` on `evangelist-acceptance-email.yml`.

> You can keep the same secret names or rename them and update the workflow accordingly.

---

## Environment example

See `.env.example` for local placeholder values matching required secrets.

---

## Customization guide

Detailed setup notes are available at:

- `docs/customization.md`

---

## Notes

- `Evangelists.md` is the list file currently watched by the welcome workflow.
- `generate_certificate.py` can use `.github/certificate-template.png` if provided, otherwise it renders a default design.
- You can add more workflows (e.g., reminder emails, rejection emails, reviewer SLA checks) based on your process.
