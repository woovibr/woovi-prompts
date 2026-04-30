# Woovi Prompts — Biblioteca de Prompts para Integração com a Woovi

Coleção de prompts em português, prontos para uso com **ferramentas de IA generativa** (Claude, ChatGPT, Lovable, Cursor, v0, Bolt, Windsurf, Copilot Workspace etc.) para gerar código de integração com a [Woovi](https://woovi.com) — a plataforma brasileira de Pix.

Cada arquivo em [`prompts/`](./prompts) contém um prompt **autocontido**, com:

- **Papel** — quem é o assistente.
- **Regra crítica** — o que ele nunca pode violar.
- **Especificação técnica** — endpoints, headers, body.
- **Regras de implementação** — restrições do Pix/Woovi (centavos, idempotência, App ID server-only).
- **Exemplos de código** — Vanilla JS, Axios, Node/Express, React, PHP.
- **Resposta esperada da API** — JSON real.
- **Formato de saída esperado** — checklist do que o código gerado deve entregar.

> Inspirado nos prompts oficiais publicados pela Woovi:
> - [Prompt para integrar com a Woovi usando IA](https://ajuda.woovi.com/hc/duvidas-frequentes/articles/1776997425-prompt-para-integrar-com-a-woovi-usando-ia)
> - [Prompt para split em subcontas](https://ajuda.woovi.com/hc/duvidas-frequentes/articles/1777388262-promp-para)
>
> Documentação oficial: <https://developers.woovi.com> e <https://developers.woovi.com/api>.

---

## Como usar

1. **Escolha** o caso de uso na tabela abaixo.
2. **Abra** o arquivo `.md` correspondente.
3. **Copie** o prompt inteiro e cole na sua ferramenta de IA preferida.
4. **Adapte** os campos comentados (App ID, URL pública do webhook, banco de dados, etc.).
5. **Revise** o código gerado seguindo o "Formato de Saída Esperado".

> Todos os prompts assumem que o App ID **fica no backend**. Se o seu cenário envolve frontend (React SDK ou JS Plugin), há uma seção específica para o **App ID público**.

---

## Índice de Prompts

### 🪙 Pix — Recebimento

| Caso de uso | Arquivo | Resumo |
|-------------|---------|--------|
| Cobrança Pix dinâmica (charge) | [`prompts/charge-pix.md`](./prompts/charge-pix.md) | `POST /charge` — gera QR + copia-e-cola, polling/webhook de status |
| QR Code Pix estático | [`prompts/pix-qrcode-static.md`](./prompts/pix-qrcode-static.md) | `POST /qrcode-static` — QR reutilizável (PDV, doação, totem) |
| Pix Automático (recorrência) | [`prompts/pix-automatico.md`](./prompts/pix-automatico.md) | `POST /subscriptions` — assinatura BCB com autorização do pagador |

### 💸 Pix — Envio (PixOut)

| Caso de uso | Arquivo | Resumo |
|-------------|---------|--------|
| PixOut consultando chave Pix | [`prompts/pixout-with-pix-key.md`](./prompts/pixout-with-pix-key.md) | `GET /pix-key/{key}` antes do `POST /transfer` — confirmação visual |
| PixOut sem consultar chave | [`prompts/pixout-without-pix-key.md`](./prompts/pixout-without-pix-key.md) | `POST /transfer` direto — payouts, reembolsos, comissões em lote |

### 🔁 Reembolso & Cliente

| Caso de uso | Arquivo | Resumo |
|-------------|---------|--------|
| Reembolso (total/parcial) | [`prompts/refund.md`](./prompts/refund.md) | `POST /refund` — devolve via `endToEndId`, suporta parciais múltiplos |
| Cadastro de pagador (customer) | [`prompts/customer.md`](./prompts/customer.md) | `POST /customer` — pré-cadastro por taxID para reuso |

### 🛰️ Webhooks

| Caso de uso | Arquivo | Resumo |
|-------------|---------|--------|
| Webhooks (todos os eventos) | [`prompts/webhooks.md`](./prompts/webhooks.md) | Cadastro, validação HMAC, idempotência, fila assíncrona |

### 🏢 Multi-conta — Subaccount, Partner, Campaign

| Caso de uso | Arquivo | Resumo |
|-------------|---------|--------|
| Subcontas + Split | [`prompts/subaccount.md`](./prompts/subaccount.md) | Marketplaces, multilojistas — `splitType: SPLIT_SUB_ACCOUNT` |
| Partner (white-label) | [`prompts/partner.md`](./prompts/partner.md) | Provisionar contas + App IDs para clientes finais |
| Campaign Pix Key | [`prompts/campaign-pix-key.md`](./prompts/campaign-pix-key.md) | Chaves Pix de afiliado/loja/campanha + comissionamento |

### 🛒 Plug-ins de E-commerce

| Plataforma | Arquivo | Resumo |
|------------|---------|--------|
| WooCommerce | [`prompts/ecommerce-woocommerce.md`](./prompts/ecommerce-woocommerce.md) | Plugin WP + hooks PHP + 5% desconto Pix |
| Magento 1 | [`prompts/ecommerce-magento1.md`](./prompts/ecommerce-magento1.md) | Módulo legacy + observer + plano de migração |
| Magento 2 | [`prompts/ecommerce-magento2.md`](./prompts/ecommerce-magento2.md) | Composer + DI plugin + observer events.xml |
| OpenCart 3 / 4 | [`prompts/ecommerce-opencart.md`](./prompts/ecommerce-opencart.md) | OCMOD + extensão Pagamentos + status mapping |
| Outras (Shopify, VTEX, Tray, Nuvemshop, Wix, PrestaShop, Bling, Tiny, RD, HubSpot…) | [`prompts/ecommerce-others.md`](./prompts/ecommerce-others.md) | Estratégias de middleware + Zapier/n8n |

### 🧩 SDKs & Plugins Frontend

| Caso de uso | Arquivo | Resumo |
|-------------|---------|--------|
| JavaScript Plugin (embed) | [`prompts/javascript-plugin.md`](./prompts/javascript-plugin.md) | `$openpix.push(["pix", ...])` + eventos `message` |
| React SDK | [`prompts/react-sdk.md`](./prompts/react-sdk.md) | `<OpenPixCheckout />`, `useOpenPix()`, Next.js (App Router) |

### 🤖 Automações & Conversação

| Canal | Arquivo | Resumo |
|-------|---------|--------|
| n8n / Zapier / Make | [`prompts/n8n-zapier.md`](./prompts/n8n-zapier.md) | HTTP Request + Webhook trigger + filtros por evento |
| WhatsApp | [`prompts/whatsapp.md`](./prompts/whatsapp.md) | Z-API, Meta Cloud API, BotConversa, SocPanel |

### 🎁 Engajamento

| Caso de uso | Arquivo | Resumo |
|-------------|---------|--------|
| Cashback (imediato + fidelidade) | [`prompts/cashback.md`](./prompts/cashback.md) | Configuração no painel + override por charge + relatório |

### 🔐 Segurança & Operação

| Caso de uso | Arquivo | Resumo |
|-------------|---------|--------|
| Autenticação, App ID, retries, auditoria | [`prompts/auth-and-security.md`](./prompts/auth-and-security.md) | Variáveis de ambiente, rotação, validação de webhook, logs auditáveis |

---

## Mapa rápido — qual prompt usar?

```
┌──────────────────────────┐
│ Quero RECEBER Pix?       │
└──────────────────────────┘
       │
       ├─ valor variável por compra .................. charge-pix.md
       ├─ QR fixo de PDV / doação .................... pix-qrcode-static.md
       └─ assinatura mensal/anual recorrente ......... pix-automatico.md

┌──────────────────────────┐
│ Quero ENVIAR Pix?        │
└──────────────────────────┘
       │
       ├─ usuário digita chave (preciso confirmar) ... pixout-with-pix-key.md
       └─ payout / reembolso programático ............ pixout-without-pix-key.md

┌──────────────────────────┐
│ Marketplace / Split?     │
└──────────────────────────┘
       │
       ├─ vendedores são meus (você titular) ......... subaccount.md
       ├─ cada cliente tem conta Woovi própria ....... partner.md
       └─ rastreio por afiliado/loja/campanha ........ campaign-pix-key.md

┌──────────────────────────┐
│ Atualizações em tempo    │
│ real?                    │
└──────────────────────────┘
       │
       └─ tudo passa por webhook ..................... webhooks.md
```

---

## Convenções dos prompts

- **Idioma:** Português (Brasil).
- **Valores:** sempre em **centavos** (inteiros).
- **`correlationID`:** UUID v4 estável → idempotência.
- **`Authorization`:** header com App ID puro, **sem** `Bearer`.
- **Backend-only:** App ID privado nunca aparece no front.
- **Webhook é fonte de verdade**, polling é só fallback.

## Stack assumida nos exemplos

- Node.js 20+ / Express / Axios — pode ser substituído por Fastify, Nest, etc.
- React 18+ / Next.js 14+ — pode ser substituído por Vue/Svelte.
- PHP 7.4+ / 8.1+ — para Magento e WooCommerce.

Os prompts são linguagem-agnósticos por design — basta pedir à IA "converta para Python/Go/Java/C#" mantendo a mesma estrutura.

## Contribuindo

1. Crie um novo `.md` em `prompts/` seguindo o template existente.
2. Adicione a linha correspondente no índice deste README.
3. Garanta que o exemplo é **executável** (App ID, valor, headers — todos preenchidos).

## Licença

MIT.
