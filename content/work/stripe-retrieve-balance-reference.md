---
# Sample 8 of 8. The reference page itself is the Markdown file in
# content/docs/stripe-retrieve-balance-reference.md; it appears in full under
# "The sample" on this page.

title: Stripe Retrieve balance API reference
summary: A practice API reference page for Stripe's Retrieve balance endpoint, written in Markdown from Stripe's public API documentation.
category: Docs as Code

date: 2026-11-06

cover: ./images/stripe-retrieve-balance-reference-cover.png
coverAlt: The top of the Retrieve balance reference page, with a practice-sample note, a short description, and the endpoint table.

role: Wrote the reference page from Stripe's public API documentation
audience: Developers integrating with Stripe's API

markdown: stripe-retrieve-balance-reference
link:
  label: View the Markdown source on GitHub
  url: https://github.com/dc-porter/Portfolio/blob/main/content/docs/stripe-retrieve-balance-reference.md
---

## Overview

This is a single-endpoint API reference page for Stripe's Retrieve balance endpoint, which returns the
money in a Stripe account that is available to pay out and the money that is still pending. It is
written for developers integrating with Stripe's API. I wrote it in Markdown as a practice sample from
Stripe's public API documentation. It is not an official Stripe document.

## My approach

The page follows the order a developer works in: what the endpoint does, how to call it, what comes
back, and what to do when it fails. Each section answers one question, with a copyable request, a full
response example, and tables for the endpoint, response fields, and errors. I explained the details
that trip people up, such as amounts in the smallest currency unit and the colon after the key in the
curl example, and kept the source in Markdown so it can be reviewed and versioned in Git like code.
