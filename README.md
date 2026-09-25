# GSX CHECK V1

Professional Telegram bot + Netlify landing page.

## What is included

- Device check menu: Apple IMEI, Apple Serial, Samsung IMEI, Universal IMEI
- IMEI Luhn validation
- Local TAC/model lookup hook
- Professional report formatting
- Honest `UNKNOWN / NOT VERIFIED` status for blacklist, stolen/lost, activation lock, carrier lock, warranty, finance, etc. until a legitimate provider API is connected
- Check packages:
  - GH₵5 = 1 check
  - GH₵10 = 3 checks
- Manual MoMo payment confirmation
- Manual crypto payment confirmation
- Digital store:
  - Apple/iTunes gift-card order workflow
  - Virtual-number order workflow
- Admin notification and inline approve/reject buttons
- Admin fulfillment buttons for digital orders
- Customer accounts and balances
- Persistent Netlify Blobs storage
- Order IDs and report IDs
- `/admin`, `/pending`, `/stats`, `/users`
- Configurable product catalog through environment variables
- Provider integration hook ready for later

## Environment variables

Required:

- `TELEGRAM_BOT_TOKEN`
- `ADMIN_USER_ID`
- `MOMO_NAME`
- `MOMO_NUMBER`

Optional crypto addresses:

- `BTC_ADDRESS`
- `USDT_TRC20_ADDRESS`
- `USDT_ERC20_ADDRESS`
- `TRX_ADDRESS`
- `ETH_ADDRESS`

Optional provider settings for later:

- `GSX_PROVIDER_URL`
- `GSX_PROVIDER_API_KEY`

Optional product catalog:

`GIFT_CARD_PRODUCTS_JSON` example:
```json
[
  {"id":"us-5","title":"Apple Gift Card US $5","price":55,"currency":"GHS","region":"US"},
  {"id":"us-10","title":"Apple Gift Card US $10","price":105,"currency":"GHS","region":"US"}
]
```

`VIRTUAL_NUMBER_PRODUCTS_JSON` example:
```json
[
  {"id":"vn-basic","title":"Virtual Number — Basic","price":30,"currency":"GHS","description":"Manual fulfillment"}
]
```

Prices are examples only. Set your actual prices and regions.

## Deploy

1. Upload this folder to a GitHub repository or deploy directly with Netlify.
2. Set the environment variables in Netlify.
3. Deploy.
4. Set Telegram webhook to:
   `https://YOUR-SITE.netlify.app/.netlify/functions/gsxcheck`
5. Open your Telegram bot and send `/start`.

Do NOT put your Telegram bot token in the code or send it to anyone.

## Important

This version does not pretend to have live GSX/Apple/GSMA data. Without an authorized data provider, the bot cannot truthfully report blacklist, stolen/lost, carrier lock, activation lock, warranty or finance status.

When you later obtain an authorized provider API, connect it inside `providerCheck()` in `netlify/functions/gsxcheck.mjs`.
