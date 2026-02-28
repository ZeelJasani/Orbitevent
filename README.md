<div align="center">

# 🚀 Orbitevent

### AI-Powered Event Management Platform

*Plan, manage, and scale exceptional events with intelligent automation.*

[![Next.js](https://img.shields.io/badge/Next.js-16-black?logo=next.js)](https://nextjs.org)
[![TypeScript](https://img.shields.io/badge/TypeScript-5-blue?logo=typescript)](https://typescriptlang.org)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-4-38bdf8?logo=tailwindcss)](https://tailwindcss.com)
[![MongoDB](https://img.shields.io/badge/MongoDB-green?logo=mongodb)](https://mongodb.com)
[![Stripe](https://img.shields.io/badge/Stripe-Payments-635bff?logo=stripe)](https://stripe.com)
[![Clerk](https://img.shields.io/badge/Clerk-Auth-6c47ff?logo=clerk)](https://clerk.com)

</div>

---

## ✨ Features

### 🤖 AI-Powered Event Generation

Generate complete event details from a single prompt using **Google Gemini AI** — auto-fills title, description, location, category, dates, and suggests multi-tiered ticket pricing.

### 🎫 Multi-Tiered Ticketing

Create unlimited ticket tiers (Early Bird, General Admission, VIP) with custom names, prices, and capacities. Each tier is independently tracked.

### 💳 Stripe Payment Integration

Secure payment processing with a robust dual-fulfillment architecture:

- **Webhook** (primary) — activates tickets after successful payment
- **Verify API** (fallback) — secondary confirmation on the success page
- Pending ticket lifecycle: `pending → active → scanned`

### 📱 QR Code Tickets & Mobile Check-in

Every purchased ticket gets a unique QR code. Organizers can scan tickets at the door using the built-in mobile check-in scanner.

### ✍️ Rich Text Editor

Event descriptions support **bold**, *italic*, headings, bullet lists, and ordered lists via the TipTap rich text editor.

### 🎨 Premium Dark UI

Vercel/Linear-inspired design system with glassmorphic navbar, smooth animations, OKLCH dark mode, and Geist typography.

---

## 🛠 Tech Stack

| Layer | Technology |
|-------|-----------|
| **Framework** | Next.js 16 (App Router, Server Actions) |
| **Language** | TypeScript 5 |
| **Styling** | Tailwind CSS 4 + Shadcn UI |
| **Authentication** | Clerk |
| **Database** | MongoDB + Mongoose |
| **Payments** | Stripe Checkout + Webhooks |
| **AI** | Google Gemini API |
| **Rich Text** | TipTap Editor |
| **QR Code** | react-qr-code + @yudiel/react-qr-scanner |

---

## 📁 Project Structure

```
orbitevent/
├── app/
│   ├── page.tsx                    # Landing page
│   ├── explore/                    # Event discovery
│   ├── create/                     # Create event (with AI)
│   ├── events/[id]/                # Event details
│   │   ├── edit/                   # Edit event
│   │   └── scan/                   # QR check-in scanner
│   ├── dashboard/                  # User dashboard
│   │   ├── tickets/                # My tickets
│   │   └── events/                 # My events
│   ├── payment/
│   │   ├── success/                # Payment success + verification
│   │   └── cancel/                 # Payment cancelled
│   └── api/
│       ├── webhook/stripe/         # Stripe webhook handler
│       └── verify-payment/         # Payment verification fallback
├── actions/                        # Server actions
│   ├── tickets.ts                  # Registration + ticket management
│   ├── queries.ts                  # Data fetching
│   ├── event.ts                    # Event CRUD
│   ├── generate.ts                 # AI event generation
│   └── scan.ts                     # QR check-in logic
├── models/                         # Mongoose schemas
│   ├── Event.ts
│   ├── Ticket.ts
│   └── User.ts
├── components/                     # UI components
│   ├── navbar.tsx
│   ├── register-button.tsx
│   ├── rich-text-editor.tsx
│   └── ui/                         # Shadcn UI primitives
└── lib/                            # Utilities
    ├── mongodb.ts                  # DB connection
    ├── stripe.ts                   # Lazy-loaded Stripe SDK
    └── utils.ts
```

## 💳 Payment Flow

```
User clicks "Buy — ₹500"
       │
       ▼
  ┌──────────┐
  │ Free?     │
  └────┬──────┘
  Yes  │  No
  │    │
  ▼    ▼
Active  Create pending ticket
ticket  + Stripe Checkout
  │         │
  ▼         ▼
Dashboard  Stripe hosted page
               │
          ┌────┴────┐
          │ Paid?    │
          └────┬────┘
          Yes  │  No
          │    │
          ▼    ▼
       Webhook  /payment/cancel
       activates  (auto-cleanup)
       ticket
          │
          ▼
       /payment/success
       (verify fallback)
```

---
