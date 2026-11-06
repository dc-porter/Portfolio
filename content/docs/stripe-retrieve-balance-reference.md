# Retrieve balance

> **Practice sample.** Written by Dairyia Porter to demonstrate API reference writing. This is not an official Stripe document. Source: Stripe's public API reference at docs.stripe.com, checked in November 2026.

Returns the current balance of your Stripe account: money that is ready to pay out and money that is still on its way. Use it to show balances in a dashboard or to check funds before you send a payout.

The balance returned belongs to the account you authenticate as.

---

## Endpoint

```http
GET https://api.stripe.com/v1/balance
```

| Item | Value |
|---|---|
| Method | `GET` (read-only; it doesn't change anything) |
| Path | `/v1/balance` |
| Authentication | Your secret or restricted API key, sent with every request |

**About keys:** Test keys start with `sk_test_` and return test data. Live keys return real data. Stripe recommends restricted keys (starting with `rk_live_`) for live mode, because they can be limited to the permissions you need. Never put a live key in documentation, screenshots, or shared code.

---

## Parameters

This endpoint takes no parameters. Send the request with your API key and nothing else.

---

## Request example

```bash
curl https://api.stripe.com/v1/balance \
  -u "sk_test_your_key_here:"
```

The `-u` option sends your API key as the username. Stripe doesn't use a password, so the colon after the key tells curl there's no password and stops it from asking for one.

---

## Response example

A successful request returns status `200 OK` and a balance object:

```json
{
  "object": "balance",
  "available": [
    {
      "amount": 666670,
      "currency": "usd",
      "source_types": {
        "card": 666670
      }
    }
  ],
  "connect_reserved": [
    {
      "amount": 0,
      "currency": "usd"
    }
  ],
  "livemode": false,
  "pending": [
    {
      "amount": 61414,
      "currency": "usd",
      "source_types": {
        "card": 61414
      }
    }
  ]
}
```

### Response fields

All amounts are in the currency's smallest unit. For US dollars, that means cents: `666670` is $6,666.70.

| Field | Type | What it means |
|---|---|---|
| `object` | string | The kind of data returned. Always `"balance"`. |
| `available` | array of objects | Money you can pay out or transfer now. One entry per currency. |
| `pending` | array of objects | Money that isn't available yet. One entry per currency. |
| `connect_reserved` | array of objects | Money held to cover negative balances on some connected accounts (Stripe Connect). Can be `null`. |
| `livemode` | boolean | `true` for real data, `false` for test data. |

Each entry in `available`, `pending`, and `connect_reserved` has these fields:

| Field | Type | What it means |
|---|---|---|
| `amount` | integer | The total for that currency, in the smallest unit. |
| `currency` | string | The three-letter currency code, in lowercase (for example, `usd`). |
| `source_types` | object | The same total, split by payment type (for example, `card`). May be missing, as in the `connect_reserved` entry in the example. |

The balance object can also include three optional fields, each of which can be `null`: `instant_available` (money you can pay out with Instant Payouts), `issuing` (money you can spend on issued cards), and `refund_and_dispute_prefunding` (money set aside to cover future refunds, disputes, or a negative balance).

---

## Errors

If the request fails, Stripe returns an error status and an `error` object explaining what went wrong:

```json
{
  "error": {
    "type": "invalid_request_error",
    "message": "Invalid API Key provided: sk_test_****1234"
  }
}
```

The errors you're most likely to see on this endpoint:

| Status | Meaning | What to do |
|---|---|---|
| `401 Unauthorized` | The API key is missing or invalid. | Check that you sent the key and copied it exactly. |
| `403 Forbidden` | The key doesn't have permission to read balances. | If you're using a restricted key, give it read access to the balance. |
| `429 Too Many Requests` | Too many requests were sent too quickly. | Wait, then retry, increasing the wait time after each attempt. |
| `500`–`504` | Something went wrong on Stripe's side. These are rare. | Retry later. |
