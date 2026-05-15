# Customization Guide

Use this repository as a template for your own contributor program.

## 1) Rename organization/program terms

After cloning, replace the following across the repository:

- `AOSSIE` → your organization name
- `Evangelists` / `Evangelist` → your program name and role title
- `evangelist-reviewer` → your reviewer file name (if you want a different name)

Also update links in the acceptance email body to your own docs/resources.

## 2) Reviewer setup

Edit:

- `.github/evangelist-reviewer`

Add one GitHub username per line for reviewers who should be mentioned/requested on applications.

## 3) Secrets required in repository settings

Set these in **Settings → Secrets and variables → Actions**:

- `AOSSIE_MAIL_USERNAME` (SMTP username/email)
- `AOSSIE_MAIL_PASSWORD` (SMTP password/app password)
- `AOSSIE_ADMIN_BCC_EMAIL` (optional admin copy recipient)

If you rename secret keys, update `.github/workflows/evangelist-acceptance-email.yml` accordingly.

## 4) Applicant information requirements

The acceptance workflow expects:

- applicant email in PR body (required)
- name/university/region if available (falls back when possible)

If your PR template is different, adjust parsing logic in:

- `.github/workflows/evangelist-acceptance-email.yml`

## 5) Test before production use

Use manual trigger:

- Workflow: `Evangelist Application — Acceptance Email`
- Event: `workflow_dispatch`

Provide test values for email/name/university/region and verify certificate + email delivery.

## 6) Optional improvements you can add

- Rejection email workflow
- Reminder workflow for unanswered application questions
- Stale application auto-close workflow
- Auto-validation of PR body format before review
