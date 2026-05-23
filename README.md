# PromptEdit — Sales Landing Page

A fully responsive sales page for **PromptEdit.com**, built with Vue 3, TypeScript, and Vite.

## Tech Stack

- Vue 3 `<script setup>` + TypeScript
- Vite
- Tailwind CSS (via `@tailwindcss/vite`)

## Getting Started

```bash
cd sales
npm install
npm run dev
```

## ngrok (Mobile Testing)

The Vite dev server is configured to accept all external hosts, so you can tunnel it directly with ngrok:

```bash
ngrok http 5173
```

No extra config needed — `allowedHosts: 'all'` is already set in `vite.config.ts`.

## Features

### Navigation
- Sticky header with top utility bar (License, Enterprise, Pricing, Login, Sign up)
- Search bar and category nav links
- **Gen AI** dropdown panel with 8 tools (ImageGen, VideoGen, MusicGen, etc.)
- Mobile hamburger menu that toggles to an ✕ when open
- Mobile Gen AI accordion with all tool options and descriptions

### Hero Section
- Large uppercase headline with green accent
- Badge pill and CTA button

### Polaroid Cards on U-Wire
- 5 cards pinned to a quadratic bezier SVG wire with a deep U shape
- Each card has a green pin, sway animation, and a video preview
- **Desktop:** hover to play video + zoom in, cards positioned absolutely along the wire
- **Mobile:** horizontal scroll-snap carousel with pin + sway preserved; tap to play video and zoom in, tap again to reset
- Water droplet animation on desktop

### Ticker Bar
- Infinite scrolling marquee of AI tool names

### Content Sections
- Intro hook with 3-column feature grid (responsive — stacks on mobile)
- "Introducing PromptEdit" dark section with AI tools grid (Image, Video, Audio, Plugins)
- Pricing section with one-time and monthly plans
- Content Creator Templates Library (100,000+ assets)
- Testimonials
- "Is this for you?" checklist with money-back guarantee
- FAQ accordion
- Footer

## Mobile Responsiveness

| Section | Mobile Behaviour |
|---|---|
| Nav | Top bar hidden, hamburger menu with Gen AI accordion |
| Polaroid cards | Horizontal scroll-snap carousel |
| Feature grid | Single column stack |
| All other grids | `auto-fit` / `minmax` — collapse naturally |
