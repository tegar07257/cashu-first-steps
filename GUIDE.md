# Cashu in 15 Minutes: Your First Private Digital Cash

*A beginner's guide to Cashu, the open-source ecash protocol for Bitcoin.*
*Written for Nut November 2026 (1–27 November 2026).*
*Author: tegar07 — first-time Cashu contributor.*

> **Honest note before you start:** this guide is **docs-based**. Every step was
> checked against the official Cashu documentation and websites on 15 November 2026,
> but it was **not tested end-to-end with real sats** — no wallet was created and no
> sats were spent while writing it. Where a detail could not be verified from the
> official docs, the guide says so explicitly. Use the test-mint practice run in
> Section 4 to try everything with zero real money.

---

## 1. What Cashu Is — and Why It Is Private

Cashu is a **free and open-source Chaumian ecash protocol built for Bitcoin**. Think of
it as digital cash: you hold bearer tokens on your own device and hand a token to
someone else the way you would hand over a banknote. There are **no accounts** — nothing
to sign up for.

Three pieces make the system work:

- **The mint.** A service (usually a Lightning node operator) that takes bitcoin in and
  issues ecash tokens, and later redeems tokens back into bitcoin. A token is an IOU:
  it represents satoshis custodied at the mint.
- **The wallet.** An app on your phone or in your browser that stores your tokens and
  talks to mints. It does *not* run a Lightning node.
- **The token.** A small piece of data — a blindly signed secret — that *is* the money.
  Whoever holds the token can spend it. Tokens can be pasted into a chat, shown as a
  QR code, or sent by email. Transfers between users of the same mint are instant and
  nearly free, and never touch Lightning.

**Why is it private?** When you deposit sats at a mint, the mint signs your token
*blindly* — it signs without seeing what it is signing, using a technique invented by
David Chaum in the 1980s. So the mint cannot link the withdrawal (when you got the
token) to the later spend (when the token is redeemed). Combined with no accounts, the
mint cannot tell who its users are or how much each one holds.

**The honest limits** (the official FAQ is upfront about these, and so should you be):

- Cashu is **custodial**: the mint holds the real sats. If a mint disappears, its tokens
  become worthless. Privacy is not the same as safety — see Section 5.
- The mint can see your **IP address** unless you use Tor or a VPN, and it can likely
  identify the *receiver* of a payment made through it (though not the sender).
- Very **large token amounts are easier to trace**, because Cashu uses fixed
  denominations and a rare large token stands out from the crowd.
- Sending a token over the internet leaves a trail in that channel. Prefer an
  end-to-end encrypted message — or, best of all, show the token as a QR code in person.

*Sources: [cashu.space](https://cashu.space), [docs.cashu.space](https://docs.cashu.space/),
[Cashu FAQ](https://docs.cashu.space/faq).*

---

## 2. Pick a Wallet

Cashu wallets are independent, open-source apps. The official list at
[cashu.space/wallets](https://cashu.space/wallets) (checked 15 November 2026) includes:

| Wallet | Platform | Best for |
|---|---|---|
| **Cashu.me** — [cashu.me](https://cashu.me) | iOS, Android, and PWA (runs in the browser) | Trying Cashu in 2 minutes with nothing to install |
| **eNuts** — [enuts.cash](https://www.enuts.cash) | iOS and Android | A full mobile wallet with contacts and multi-mint swaps |
| **Minibits** — [minibits.cash](https://www.minibits.cash) | iOS and Android | Mobile-first use (listed on cashu.space; button-level steps not verified from its docs) |
| **Macadamia** — [macadamia.cash](https://macadamia.cash) | iOS only | iPhone users who want a native app |

**My recommendation for a first-timer: Cashu.me.** Open [cashu.me](https://cashu.me) in
your browser and add it to your home screen to install it as a progressive web app
(PWA). No download, no account, no setup form. Its release notes warn, correctly,
that ecash is a bearer instrument: if you delete your browser data or lose the device
without a backup, you lose your funds — so use it only for small spending amounts.

**If you prefer a native phone app, eNuts** is the most documented alternative: its
official FAQ covers receiving and redeeming tokens, sending to contacts, multi-mint
swaps, seed recovery, and troubleshooting. Minibits and Macadamia are real, actively
listed wallets too — but their button-by-button flows were not verified from their own
docs for this guide, so they are listed here without step-by-step instructions.

*Sources: [cashu.space/wallets](https://cashu.space/wallets),
[Cashu.me release notes](https://gist.github.com/callebtc/67da3f586ef273df80bf679e464bc3f3),
[eNuts FAQ](https://www.enuts.cash/faqs).*

---

## 3. Pick a Mint — and Check Its Reputation

A mint is the one party you must trust, so choose deliberately. A mint is not
"Cashu itself" — it is an independent operator, and anyone can run one.

**How to find mints:** browse the community lists the official FAQ points to,
[cashumints.space](https://cashumints.space) and [bitcoinmints.com](https://bitcoinmints.com),
or discover mints via Nostr reviews inside Cashu.me.

**How to vet a mint before you trust it with real sats:**

1. **Know the operator.** Prefer a mint run by a person or project you recognise, with
   a public reputation. The eNuts FAQ warns that mints "may be established and
   dismantled regularly without prior notice" and that scammers exploit this — verify
   a mint's reputation before interacting with it.
2. **Check it is actually online.** The eNuts FAQ gives a concrete test: paste the
   mint's URL into your browser and add `/keys` at the end. If the page shows a list
   of keys, the mint is operational.
3. **Check the fees.** Mints may charge fees; eNuts shows them before you confirm a
   transaction, so read that screen instead of tapping through.
4. **Start small.** Put in a tiny amount first, send a token to yourself or a friend,
   and redeem it back — before trusting the mint with anything larger.

**Practice for free first.** The official FAQ lists two **test mints** with unbacked,
fake ecash for testing: `https://testnut.cashu.space` (charges fees) and
`https://nofees.testnut.cashu.space` (no fees). Their tokens are worthless by design —
the safest place to make your first mistakes.

**Not yet verified:** this guide does not recommend any specific production mint by
name, because mint quality changes over time and no official "trusted mint" ranking
exists in the docs.

*Sources: [Cashu FAQ](https://docs.cashu.space/faq),
[eNuts FAQ](https://www.enuts.cash/faqs),
[Cashu.me release notes](https://gist.github.com/callebtc/67da3f586ef273df80bf679e464bc3f3).*

---

## 4. Your First Ecash: Receive, Send, and Cash Out

You need only three moves to complete the loop. Do the whole loop first on a test mint
(Section 3) so your first real run is boring — boring is good.

### Step 1 — Add a mint to your wallet

Open your wallet, go to its mint section, and paste the mint's URL. In Cashu.me the
mint tab on the home screen lets you add and edit mints, and your active mint is shown
under your main balance. That mint is now where your tokens for this wallet live.

### Step 2 — Receive your first ecash

There are two ways in, and you will probably use both:

- **Someone sends you a token.** A token is just text (often shown as a QR code).
  Copy it or scan it, then redeem it. In eNuts: press **Receive**, then **Redeem
  Ecash**. In Cashu.me, you can also create a **payment request**: first enable it in
  **Settings → Payment requests** (optionally also *Claim automatically*), then press
  **Receive → Ecash → Request**.
- **Mint ecash from Lightning.** Ask your wallet to mint a chosen amount of sats; it
  gets a Lightning invoice from the mint, and you pay that invoice from any Lightning
  wallet you already use. Once the payment confirms, the mint issues ecash tokens to
  your wallet. **Not yet verified:** the exact button labels for this flow differ
  between wallets and versions, so follow your wallet's on-screen prompts.

### Step 3 — Send ecash to someone else

Pick an amount, and your wallet creates a token for exactly that amount. Share it as
a QR code or pasted text over an encrypted channel. The receiver redeems it in their
own wallet (Step 2). In eNuts you can also send to a saved contact: press **Send** and
choose a contact (contacts are added by Nostr public key). Remember: a token is bearer
cash — **anyone who sees the token text can redeem it**, so never post one publicly.

### Step 4 — Cash out (optional, but complete the loop once)

To turn ecash back into bitcoin, your wallet "melts" the token: it pays a Lightning
invoice of your choice from the mint. Try melting a tiny amount on the test mint first,
so you know the exit works before you need it.

**One hard rule:** tokens belong to one mint only. You cannot receive a token from
Mint A into Mint B. To move value between mints, use the wallet's **Multimint Swap**
function, which swaps via a Lightning transaction (routing fees may apply).

*Sources: [Cashu FAQ](https://docs.cashu.space/faq),
[eNuts FAQ](https://www.enuts.cash/faqs).*

---

## 5. Stay Safe: Five Rules That Matter More Than the Technology

1. **A mint can rug-pull. Never store large amounts.** Ecash is a claim on the mint,
   not a deposit in a vault. The official FAQ says it plainly: "Don't put any money
   into Cashu mints/wallets that you're not willing to lose." Small spending amounts
   only.
2. **Back up your seed — on paper, offline.** Your wallet gives you a seed phrase.
   Write it down by hand and keep it somewhere safe; never type it into a website or
   a Google Form, and never share it with "support" — real support will never ask for
   it. Losing your seed means nobody can help you recover the wallet.
3. **Know the limits of seed recovery.** A seed can restore your wallet in a different
   Cashu app (standardised in NUT-13), but with two catches the FAQ spells out: your
   seed only restores ecash minted or received *after* the seed was generated, and you
   must manually re-add each mint — there is no automatic mint discovery. And recovery
   only works if the mint is still operational: in the words of the eNuts FAQ,
   "without the mint, you cannot access or restore your funds."
4. **Protect the device that holds the tokens.** In a browser wallet like Cashu.me,
   your tokens live in browser local storage — clearing browser data wipes them. Do
   not open the same wallet in multiple browser tabs (the FAQ warns against this), and
   back up before you switch devices or reinstall anything.
5. **Remember this is young software.** Cashu wallets and tools are still in early
   development; funds can be lost to bugs in the software or the protocol. That is not
   a reason to avoid Cashu — it is a reason to learn it with test mints and pocket
   money first.

*Sources: [Cashu FAQ](https://docs.cashu.space/faq),
[eNuts FAQ](https://www.enuts.cash/faqs).*

---

## 6. Where to Go Next

- **Start here:** [cashu.space](https://cashu.space) — the project home page.
- **Learn the protocol:** [docs.cashu.space](https://docs.cashu.space/) and the
  [FAQ](https://docs.cashu.space/faq).
- **Find a wallet:** [cashu.space/wallets](https://cashu.space/wallets).
- **Find a mint:** [cashumints.space](https://cashumints.space),
  [bitcoinmints.com](https://bitcoinmints.com).
- **Practice with fake ecash:** [testnut.cashu.space](https://testnut.cashu.space)
  (with fees) and [nofees.testnut.cashu.space](https://nofees.testnut.cashu.space)
  (no fees).
- **Read the spec:** the Cashu NUTs (Notation, Usage, Terminology) at
  [github.com/cashubtc/nuts](https://github.com/cashubtc/nuts).
- **Build with Cashu:** libraries include Nutshell (Python), CDK (Rust), Cashu TS
  (TypeScript), and Coco (TypeScript) — see
  [cashu.space/wallets](https://cashu.space/wallets).
- **The hackathon:** [nutnovember.org](https://nutnovember.org/) — submissions close
  **27 November 2026, 23:59 UTC**; winners announced 30 November 2026.

---

## Glossary

- **Ecash** — digital bearer money: whoever holds the token owns the value, like a
  banknote. No account needed.
- **Cashu** — the open-source Chaumian ecash protocol for Bitcoin.
- **Mint** — a service that issues ecash tokens against Lightning payments and redeems
  them back into bitcoin. Custodial: it holds the real sats.
- **Wallet** — the app that stores your tokens and talks to mints. It is not a
  Lightning wallet and does not run a Lightning node.
- **Token (a "nut")** — a piece of data consisting of a blindly signed secret; an IOU
  for a specific amount of sats at a specific mint.
- **Blind signature** — a signature made without the signer seeing what is signed,
  which breaks the link between issuing a token and spending it.
- **Sats** — satoshis, the smallest unit of bitcoin (100,000,000 sats = 1 BTC).
- **Mint (verb) / melt** — to *mint* is to turn Lightning sats into ecash tokens; to
  *melt* is to turn tokens back into a Lightning payment.
- **Multimint Swap** — moving value between two different mints via Lightning.
- **Seed phrase** — the words that let you restore your wallet in another Cashu app
  (standardised in NUT-13).
- **NUTs** — Notation, Usage, Terminology: the Cashu protocol specifications.
- **PWA** — progressive web app: a website installable on your phone like an app.

---

*Guide prepared for Nut November 2026. All sources accessed 15 November 2026.
Cashu is early-stage software — verify anything that moves real money against the
current official docs before you act.*
