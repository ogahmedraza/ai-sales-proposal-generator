# AI Sales Proposal Generator

> Turn a qualified lead payload into a structured Google Docs proposal, then send the document link to Telegram.

## The problem

Writing proposals from scattered notes is slow and inconsistent. This workflow accepts a defined lead payload, rejects incomplete requests early, and produces a proposal document from the data actually supplied.

## What this workflow does

```text
POST webhook
  → normalize input
  → validate required fields
  → generate proposal text with OpenAI
  → create and populate a Google Doc
  → send the document link to Telegram
  → return a JSON result
```

Invalid requests receive a separate `400` response and an alert. Runtime failures follow their own error route and return `500`; they are not silently treated as successful proposals.

## Required webhook fields

| Field | Purpose |
| --- | --- |
| `client_name` | Proposal recipient |
| `service` | Offer being proposed |
| `requirements` | Client problem or project brief |
| `timeline` | Delivery timeline |
| `price` | Investment amount |
| `telegram_chat_id` | Destination for the completed document link |

Optional fields include `company_name`, `client_email`, `deliverables`, `currency`, `payment_terms`, `support_terms`, `validity`, and `seller_name`.

## Example request

```json
{
  "client_name": "Alex Morgan",
  "company_name": "Northstar Services",
  "service": "Lead follow-up automation",
  "requirements": "Qualify website enquiries and send the team a daily summary",
  "timeline": "14 days",
  "price": "850",
  "currency": "USD",
  "telegram_chat_id": "YOUR_TELEGRAM_CHAT_ID"
}
```

## Before activation

1. Import `workflow.json` into n8n.
2. Connect OpenAI, Google Docs, and Telegram with your own credentials.
3. Set the webhook URL and use a private Telegram chat ID.
4. Review prompt wording, field mappings, document ownership, and error notifications.
5. Test with non-client sample data before exposing the webhook.

## Practical boundaries

- The AI receives only the submitted lead fields; it should not invent scope, guarantees, pricing, or case studies.
- The Google document is created in the connected account, so document-sharing rules are your responsibility.
- This repository is a sanitized workflow template. It contains no credentials, client data, or live document IDs.

## Files

| File | Description |
| --- | --- |
| `workflow.json` | Importable n8n workflow |
| `LICENSE` | MIT license |
| `SECURITY.md` | Security reporting guidance |

## License

MIT — see [LICENSE](LICENSE).