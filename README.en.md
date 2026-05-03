# Woovi Prompts — Prompt Library for Woovi Integration

> 🌐 **Languages:** [Português](./README.md) · **English (this file)**
>
> Prompts are available in two folders: [`prompts/`](./prompts) (PT-BR) and [`prompts-en/`](./prompts-en) (EN). Technical content is identical — pick whichever language your team/AI prefers.

A collection of English-language prompts, ready to use with **generative AI tools** (Claude, ChatGPT, Lovable, Cursor, v0, Bolt, Windsurf, Copilot Workspace, etc.) to generate integration code for [Woovi](https://woovi.com) — the Brazilian Pix platform.

Each file in [`prompts-en/`](./prompts-en) contains a **self-contained** prompt with:

- **Role** — who the assistant is.
- **Critical Rule** — what it must never violate.
- **Technical Specification** — endpoints, headers, body.
- **Implementation Rules** — Pix/Woovi constraints (cents, idempotency, server-only App ID).
- **Code Examples** — Vanilla JS, Axios, Node/Express, React, PHP.
- **Expected API Response** — real JSON.
- **Expected Output Format** — checklist of what the generated code must deliver.

> Inspired by the official prompts published by Woovi:
> - [Prompt to integrate with Woovi using AI](https://ajuda.woovi.com/hc/duvidas-frequentes/articles/1776997425-prompt-para-integrar-com-a-woovi-usando-ia)
> - [Prompt for split into subaccounts](https://ajuda.woovi.com/hc/duvidas-frequentes/articles/1777388262-promp-para)
>
> Official documentation: <https://developers.woovi.com> and <https://developers.woovi.com/api>.

---

## How to use

1. **Choose** the use case from the table below.
2. **Open** the corresponding `.md` file.
3. **Copy** the entire prompt and paste it into your preferred AI tool.
4. **Adapt** the commented fields (App ID, public webhook URL, database, etc.).
5. **Review** the generated code following the "Expected Output Format".

> All prompts assume the App ID **lives on the backend**. If your scenario involves frontend (React SDK or JS Plugin), there's a specific section for the **public App ID**.

---

## Prompt Index

### 🪙 Pix — Receiving

| Use case | File | Summary |
|----------|------|---------|
| Dynamic Pix charge | [`prompts-en/charge-pix.md`](./prompts-en/charge-pix.md) | `POST /charge` — generates QR + copy-and-paste, status polling/webhook |
| Static Pix QR Code | [`prompts-en/pix-qrcode-static.md`](./prompts-en/pix-qrcode-static.md) | `POST /qrcode-static` — reusable QR (POS, donations, kiosk) |
| Pix Automático (recurring) | [`prompts-en/pix-automatico.md`](./prompts-en/pix-automatico.md) | `POST /subscriptions` — BCB subscription with payer authorization |

### 💸 Pix — Sending (PixOut)

| Use case | File | Summary |
|----------|------|---------|
| PixOut with Pix-key lookup | [`prompts-en/pixout-with-pix-key.md`](./prompts-en/pixout-with-pix-key.md) | `GET /pix-key/{key}` before `POST /transfer` — visual confirmation |
| PixOut without lookup | [`prompts-en/pixout-without-pix-key.md`](./prompts-en/pixout-without-pix-key.md) | `POST /transfer` direct — payouts, refunds, batch commissions |

### 🔁 Refund & Customer

| Use case | File | Summary |
|----------|------|---------|
| Refund (full/partial) | [`prompts-en/refund.md`](./prompts-en/refund.md) | `POST /refund` — refund via `endToEndId`, supports multiple partials |
| Customer (payer) registration | [`prompts-en/customer.md`](./prompts-en/customer.md) | `POST /customer` — pre-registration by taxID for reuse |

### 🛰️ Webhooks

| Use case | File | Summary |
|----------|------|---------|
| Webhooks (all events) | [`prompts-en/webhooks.md`](./prompts-en/webhooks.md) | Registration, HMAC validation, idempotency, async queue |

### 🏢 Multi-account — Subaccount, Partner, Campaign

| Use case | File | Summary |
|----------|------|---------|
| Subaccounts + Split | [`prompts-en/subaccount.md`](./prompts-en/subaccount.md) | Marketplaces, multi-seller — `splitType: SPLIT_SUB_ACCOUNT` |
| Partner (white-label) | [`prompts-en/partner.md`](./prompts-en/partner.md) | Provision accounts + App IDs for end customers |
| Campaign Pix Key | [`prompts-en/campaign-pix-key.md`](./prompts-en/campaign-pix-key.md) | Pix keys for affiliate/store/campaign + commission tracking |

### 🛒 E-commerce Plugins

| Platform | File | Summary |
|----------|------|---------|
| WooCommerce | [`prompts-en/ecommerce-woocommerce.md`](./prompts-en/ecommerce-woocommerce.md) | WP plugin + PHP hooks + 5% Pix discount |
| Magento 1 | [`prompts-en/ecommerce-magento1.md`](./prompts-en/ecommerce-magento1.md) | Legacy module + observer + migration plan |
| Magento 2 | [`prompts-en/ecommerce-magento2.md`](./prompts-en/ecommerce-magento2.md) | Composer + DI plugin + observer events.xml |
| OpenCart 3 / 4 | [`prompts-en/ecommerce-opencart.md`](./prompts-en/ecommerce-opencart.md) | OCMOD + Payments extension + status mapping |
| Others (Shopify, VTEX, Tray, Nuvemshop, Wix, PrestaShop, Bling, Tiny, RD, HubSpot…) | [`prompts-en/ecommerce-others.md`](./prompts-en/ecommerce-others.md) | Middleware strategies + Zapier/n8n |

### 🧩 SDKs & Frontend Plugins

| Use case | File | Summary |
|----------|------|---------|
| JavaScript Plugin (embed) | [`prompts-en/javascript-plugin.md`](./prompts-en/javascript-plugin.md) | `$openpix.push(["pix", ...])` + `message` events |
| React SDK | [`prompts-en/react-sdk.md`](./prompts-en/react-sdk.md) | `<OpenPixCheckout />`, `useOpenPix()`, Next.js (App Router) |

### 🤖 Automations & Conversation

| Channel | File | Summary |
|---------|------|---------|
| n8n / Zapier / Make | [`prompts-en/n8n-zapier.md`](./prompts-en/n8n-zapier.md) | HTTP Request + Webhook trigger + per-event filters |
| WhatsApp | [`prompts-en/whatsapp.md`](./prompts-en/whatsapp.md) | Z-API, Meta Cloud API, BotConversa, SocPanel |

### 🎁 Engagement

| Use case | File | Summary |
|----------|------|---------|
| Cashback (immediate + loyalty) | [`prompts-en/cashback.md`](./prompts-en/cashback.md) | Dashboard configuration + per-charge override + report |

### 🔐 Security & Operations

| Use case | File | Summary |
|----------|------|---------|
| Authentication, App ID, retries, audit | [`prompts-en/auth-and-security.md`](./prompts-en/auth-and-security.md) | Environment variables, rotation, webhook validation, auditable logs |

---

## Quick map — which prompt to use?

```
┌──────────────────────────┐
│ I want to RECEIVE Pix?   │
└──────────────────────────┘
       │
       ├─ variable amount per purchase ............... charge-pix.md
       ├─ fixed QR for POS / donation ................ pix-qrcode-static.md
       └─ recurring monthly/yearly subscription ...... pix-automatico.md

┌──────────────────────────┐
│ I want to SEND Pix?      │
└──────────────────────────┘
       │
       ├─ user types key (need confirmation) ......... pixout-with-pix-key.md
       └─ programmatic payout / refund ............... pixout-without-pix-key.md

┌──────────────────────────┐
│ Marketplace / Split?     │
└──────────────────────────┘
       │
       ├─ sellers are mine (you are the holder) ...... subaccount.md
       ├─ each customer has their own Woovi account .. partner.md
       └─ track by affiliate/store/campaign .......... campaign-pix-key.md

┌──────────────────────────┐
│ Real-time updates?       │
└──────────────────────────┘
       │
       └─ everything goes through webhook ............ webhooks.md
```

---

## Prompt conventions

- **Language:** English (this folder) / Brazilian Portuguese (in [`prompts/`](./prompts)).
- **Values:** always in **cents** (integers).
- **`correlationID`:** stable UUID v4 → idempotency.
- **`Authorization`:** header with raw App ID, **without** `Bearer`.
- **Backend-only:** the private App ID never appears on the frontend.
- **Webhook is the source of truth**, polling is only a fallback.

## Stack assumed in the examples

- Node.js 20+ / Express / Axios — can be swapped for Fastify, Nest, etc.
- React 18+ / Next.js 14+ — can be swapped for Vue/Svelte.
- PHP 7.4+ / 8.1+ — for Magento and WooCommerce.

The prompts are language-agnostic by design — just ask the AI to "convert to Python/Go/Java/C#" while keeping the same structure.

## Contributing

1. Create a new `.md` under `prompts-en/` (and ideally a matching one under `prompts/`) following the existing template.
2. Add the corresponding line to the index in this README (and the Portuguese README).
3. Make sure the example is **runnable** (App ID, value, headers — all filled in).

## License

MIT.
