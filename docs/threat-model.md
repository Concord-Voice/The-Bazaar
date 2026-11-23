# Threat model — The-Bazaar

| Field | Value |
| --- | --- |
| Repository | Concord-Voice/The-Bazaar |
| Visibility | Public |
| Last reviewed | 2026-11-23 at commit `09b374e` |
| Owner | Concord Voice maintainers |
| Review when | Before the first feature merges; then on any change to authentication, a trust boundary, or exposed surface |

**Status: placeholder.** This repository ships no code. Every statement below about the
future marketplace is an expectation, not a verified fact. Write the full model before the
first feature merges.

## System summary

The Bazaar is the planned community marketplace for Concord Voice add-ons: themes, sound
packs, bots and other add-ons, free to install, with an optional donation link for each
creator (`README.md`). Today the repository holds a README and one code-quality workflow
(`.github/workflows/sonarcloud.yml`). There is no production deployment.

## Assets

None in production. Expected: the integrity of each listed add-on, creator identity, the
integrity of donation links, and the trust users place in a listing.

## Adversaries

Today: a compromised dependency or CI input, and a contributor who changes the workflow.
Expected: a malicious creator, a creator whose account is taken over, and an anonymous
visitor who abuses listing or search.

## Attack surface

Today: pull requests and the workflow in `.github/workflows/sonarcloud.yml`. Expected:
add-on upload and review, add-on install into a client, listing pages, donation links.

## Trust boundaries

Today: contributor to repository. Branch protection and required review are assumed; this repository holds nothing that confirms them. Expected:
creator to marketplace, marketplace to client, add-on to the client that runs it.

## Security objectives

Expected: a client installs only an add-on that the marketplace published and that has not
changed since; an add-on gets no access to message content or key material; a donation link
goes where the creator set it.

## Attack paths

Hypotheses, to be ranked when a design exists: a malicious add-on that runs code in the
client (A03 Software Supply Chain Failures, A08 Software or Data Integrity Failures); a
listing takeover that swaps a trusted add-on (A01 Broken Access Control, A07 Authentication
Failures); a donation link replaced with an attacker's (A01 Broken Access Control).

## Weakest ground

Not assessed. The largest expected risk is that add-ons are third-party code or content
that runs inside an end-to-end-encrypted client.

## Hardening and surface reduction

Decide before any code: what an add-on may do in a client, how an add-on is signed and
reviewed, and whether bots run with a user's authority or their own.

## Assumptions and unknowns

The design, hosting, and data handled are all unknown. No personal data is processed today.

## Standards alignment

| Framework | What it prioritises here |
| --- | --- |
| OWASP Top 10:2025 | A03 and A08: the marketplace is a software supply chain into the clients |
| NIST CSF 2.0 | GV Govern and ID Identify: set the add-on trust policy before building |

All frameworks are alignment targets. Nothing here is a claim of compliance or certification.
