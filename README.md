# AI Sales Proposal Generator

An n8n workflow that validates lead data, generates a structured sales proposal with OpenAI, creates the proposal in Google Docs, and sends the result through Telegram.

## Flow

Webhook → Validation → OpenAI proposal → Google Docs → Telegram

## Included

- Input validation and normalized lead data
- AI-generated proposal content
- Google Docs proposal creation and writing
- Telegram delivery
- Success, bad-request, and input-error paths

## Setup

Import workflow.json into n8n, then connect your own OpenAI, Google Docs, and Telegram credentials. Review every prompt, field mapping, webhook path, and notification destination before activating it.

This is a demo workflow and contains no credentials or client data.
