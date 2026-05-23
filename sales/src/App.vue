<script setup lang="ts">
const cards = [
  { label: 'AI Prompts',  sub: 'Generate prompts for any AI model', bg: '#f472b6', rotate: '-6deg', top: '0px',
    video: 'https://videos.pexels.com/video-files/3129671/3129671-hd_1920_1080_30fps.mp4', iframe: '' },
  { label: 'Veo 3',       sub: 'Cinematic AI video generations',     bg: '#a3e635', rotate: '-3deg', top: '0px',
    video: 'https://www.pexels.com/download/video/18069701/', iframe: '' },
  { label: 'Templates',   sub: 'DaVinci & Premiere Pro packs',       bg: '#22d3ee', rotate: '0deg',  top: '-12px',
    video: 'https://www.pexels.com/download/video/31723814/', iframe: '' },
  { label: 'KlingAI',     sub: 'Ready-to-use prompt bundles',        bg: '#fb923c', rotate: '3deg',  top: '0px',
    video: 'https://www.pexels.com/download/video/36380551/', iframe: '' },
  { label: 'Geography',   sub: 'Sell your work worldwide',           bg: '#1e293b', rotate: '6deg',  top: '18px',
    video: 'https://www.pexels.com/download/video/2695085/', iframe: '' },
]

const genAiTools = [
  { emoji: '🖼️', name: 'ImageGen',    desc: 'Create unique visuals in diverse styles with simple text prompts.' },
  { emoji: '✏️', name: 'ImageEdit',   desc: 'Remove backgrounds, erase objects & upscale effortlessly.' },
  { emoji: '🎬', name: 'VideoGen',    desc: 'Generate videos from static images and text prompts.' },
  { emoji: '🎵', name: 'MusicGen',    desc: 'Make your own music with text prompts and presets.' },
  { emoji: '🎙️', name: 'VoiceGen',    desc: 'Turn your text into professional voiceovers & let AI do the talking.' },
  { emoji: '🔊', name: 'SoundGen',    desc: 'Get pro-quality sound effects to purpose-fit your project.' },
  { emoji: '🎨', name: 'GraphicsGen', desc: 'Craft icons and illustrations with a reference style and text prompt.' },
  { emoji: '📦', name: 'MockupGen',   desc: 'Create custom mockups in minutes.' },
]

import { ref, onMounted, onUnmounted } from 'vue'
const aiOpen = ref(false)
const mobileOpen = ref(false)
const mobileAiOpen = ref(false)

function closeAi() { aiOpen.value = false }
onMounted(() => document.addEventListener('click', closeAi))
onUnmounted(() => document.removeEventListener('click', closeAi))

const touchedCard = ref<string | null>(null)

function onCardTouch(id: string, el: HTMLElement) {
  const prev = touchedCard.value
  // reset previous card's video if different
  if (prev && prev !== id) {
    const prevEl = document.querySelector(`[data-card-id="${prev}"]`) as HTMLElement | null
    if (prevEl) {
      const v = prevEl.querySelector('video') as HTMLVideoElement | null
      if (v) { v.pause(); v.currentTime = 0 }
    }
  }
  if (touchedCard.value === id) {
    // second touch — reset
    const v = el.querySelector('video') as HTMLVideoElement | null
    if (v) { v.pause(); v.currentTime = 0 }
    touchedCard.value = null
  } else {
    const v = el.querySelector('video') as HTMLVideoElement | null
    if (v) { v.load(); v.play() }
    touchedCard.value = id
  }
}

const swayDelay = ['0s','0.6s','1.2s','1.8s','2.4s']
const logos = ['Seedance 2.0 Text to Video','Seedance 2.0 Image to Video','ElevenLabs Voice Changer','ElevenLabs TTS','HeyGen Avatar 4','Kling V3','Grok Imagine','Suno V4.5','Kling O1 Edit','Kling V2.6','Kling Motion Control','Kling V2.5 Turbo','Kling V2.1 Master','Veo 3.1','Veo 3.1 Fast','Nano Banana Pro','Sora 2','Sora 2 Pro','ElevenLabs Text to Sound','Nano Banana','Grok Imagine Edit','Topaz Upscale','Seedance 2.0 Fast Text to Video','Seedance 2.0 Fast Image to Video','Seedance 2.0 Text to Video','Seedance 2.0 Image to Video','ElevenLabs Voice Changer','ElevenLabs TTS','HeyGen Avatar 4','Kling V3','Grok Imagine','Suno V4.5','Kling O1 Edit','Kling V2.6','Kling Motion Control','Kling V2.5 Turbo','Kling V2.1 Master','Veo 3.1','Veo 3.1 Fast','Nano Banana Pro','Sora 2','Sora 2 Pro','ElevenLabs Text to Sound','Nano Banana']
</script>

<template>
  <div style="min-height:100vh;background:radial-gradient(ellipse at 50% 0%,#e8f5e9 0%,#f5f5e8 40%,#fafaf5 100%);font-family:'Inter',sans-serif;overflow-x:hidden;">

    <!-- ═══ NAV ═══ -->
    <header class="site-header">

      <!-- Top utility bar -->
      <div class="nav-top">
        <div class="nav-top-inner">
          <div class="nav-top-left">
            <a href="#">License</a>
            <a href="#">Enterprise</a>
            <a href="#">Pricing</a>
          </div>
          <div class="nav-top-right">
            <a href="#" class="nav-login">Log in</a>
            <a href="#" class="nav-signup">Sign up free</a>
            <a href="#" class="nav-unlimited">✦ Get unlimited downloads</a>
          </div>
        </div>
      </div>

      <!-- Main nav -->
      <nav class="nav-main">
        <!-- Logo -->
        <a href="#" class="nav-logo">
          <span class="logo-dot">●</span>PromptEdit
        </a>

        <!-- Search -->
        <div class="nav-search-bar">
          <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="11" cy="11" r="8"/><path d="m21 21-4.35-4.35"/></svg>
          <input type="text" placeholder="Search millions of assets…" />
        </div>

        <!-- Hamburger (mobile only) -->
        <button class="nav-hamburger" @click.stop="mobileOpen = !mobileOpen" aria-label="Toggle menu">
          <span :class="{ 'bar-open': mobileOpen }"></span>
          <span :class="{ 'bar-open-mid': mobileOpen }"></span>
          <span :class="{ 'bar-open': mobileOpen }"></span>
        </button>

        <!-- Category links -->
        <div class="nav-links">
          <!-- Gen AI dropdown trigger -->
          <button
            class="nav-link nav-link-ai"
            @click.stop="aiOpen = !aiOpen"
          >✦ Gen AI <span class="ai-chevron" :class="{ open: aiOpen }">▾</span></button>
          <a href="#" class="nav-link">Video Templates</a>
          <a href="#" class="nav-link">Stock Video</a>
          <a href="#" class="nav-link">Audio</a>
          <a href="#" class="nav-link">Graphics</a>
          <a href="#" class="nav-link">Design Templates</a>
          <a href="#" class="nav-link">Photos</a>
          <a href="#" class="nav-link">3D</a>
          <a href="#" class="nav-link">Fonts</a>
          <a href="#" class="nav-link">Web</a>
        </div>
      </nav>

      <!-- Gen AI dropdown panel — full-width horizontal bar -->
      <div v-show="aiOpen" class="ai-dropdown-panel" @click.stop>
        <a href="#" class="ai-dropdown-item" v-for="tool in genAiTools" :key="tool.name">
          <span class="ai-item-emoji">{{ tool.emoji }}</span>
          <div>
            <p class="ai-item-name">{{ tool.name }}</p>
            <p class="ai-item-desc">{{ tool.desc }}</p>
          </div>
        </a>
      </div>
      <!-- Mobile menu -->
      <transition name="menu-slide">
        <div v-show="mobileOpen" class="mobile-menu" @click.stop>

          <!-- ── Utility links ── -->
          <div class="mm-utility">
            <a href="#" class="mm-util-link">License</a>
            <a href="#" class="mm-util-link">Enterprise</a>
            <a href="#" class="mm-util-link">Pricing</a>
          </div>

          <!-- ── Nav links ── -->
          <div class="mm-nav-links">
            <!-- Gen AI accordion -->
            <button class="mm-link mm-ai-toggle" @click="mobileAiOpen = !mobileAiOpen">
              <span class="mm-ai-label"><span class="mm-ai-star">✦</span> Gen AI</span>
              <span class="ai-chevron" :class="{ open: mobileAiOpen }">▾</span>
            </button>
            <transition name="submenu-slide">
              <div v-show="mobileAiOpen" class="mobile-ai-submenu">
                <a href="#" class="mobile-ai-item" v-for="tool in genAiTools" :key="tool.name">
                  <span class="mobile-ai-emoji">{{ tool.emoji }}</span>
                  <div>
                    <p class="ai-item-name">{{ tool.name }}</p>
                    <p class="ai-item-desc" style="text-align:left;">{{ tool.desc }}</p>
                  </div>
                </a>
              </div>
            </transition>
            <a href="#" class="mm-link">Video Templates</a>
            <a href="#" class="mm-link">Stock Video</a>
            <a href="#" class="mm-link">Audio</a>
            <a href="#" class="mm-link">Graphics</a>
            <a href="#" class="mm-link">Design Templates</a>
            <a href="#" class="mm-link">Photos</a>
            <a href="#" class="mm-link">3D</a>
            <a href="#" class="mm-link">Fonts</a>
            <a href="#" class="mm-link">Web</a>
          </div>

          <!-- ── Auth buttons ── -->
          <div class="mm-auth">
            <a href="#" class="mm-login">Log in</a>
            <a href="#" class="mm-signup">Sign up free</a>
          </div>

          <!-- ── CTA ── -->
          <div class="mm-cta-wrap">
            <a href="#" class="mm-cta">✦ Get unlimited downloads</a>
          </div>

        </div>
      </transition>
    </header>

    <!-- ═══ HERO ═══ -->
    <section class="hero-section">

      <!-- ── Mobile cinematic background (mobile only) ── -->
      <div class="mobile-hero-bg" aria-hidden="true">
        <!-- Colour orbs that bloom open -->
        <div class="orb orb-1"></div>
        <div class="orb orb-2"></div>
        <div class="orb orb-3"></div>
        <div class="orb orb-4"></div>
        <!-- Light rays -->
        <div class="ray ray-1"></div>
        <div class="ray ray-2"></div>
        <div class="ray ray-3"></div>
        <!-- Floating sparkles -->
        <div class="spark spark-1"></div>
        <div class="spark spark-2"></div>
        <div class="spark spark-3"></div>
        <div class="spark spark-4"></div>
        <div class="spark spark-5"></div>
        <!-- Camera -->
        <div class="cam-wrap">
          <svg class="cam-svg" viewBox="0 0 120 90" fill="none" xmlns="http://www.w3.org/2000/svg">
            <!-- body -->
            <rect x="8" y="22" width="104" height="62" rx="10" fill="#111" stroke="#22c55e" stroke-width="2.5"/>
            <!-- viewfinder bump -->
            <rect x="38" y="10" width="44" height="16" rx="6" fill="#111" stroke="#22c55e" stroke-width="2"/>
            <!-- lens outer ring -->
            <circle cx="60" cy="53" r="22" fill="#1a1a1a" stroke="#22c55e" stroke-width="2.5"/>
            <!-- lens mid ring -->
            <circle cx="60" cy="53" r="15" fill="#0f0f0f" stroke="rgba(34,197,94,0.4)" stroke-width="1.5"/>
            <!-- lens inner -->
            <circle cx="60" cy="53" r="8" fill="#22c55e" opacity="0.9"/>
            <!-- lens shine -->
            <circle cx="56" cy="49" r="2.5" fill="white" opacity="0.5"/>
            <!-- shutter button -->
            <circle cx="96" cy="34" r="5" fill="#22c55e"/>
            <!-- flash -->
            <rect x="14" y="28" width="12" height="8" rx="3" fill="#fbbf24" opacity="0.85"/>
          </svg>
          <!-- shutter flash overlay -->
          <div class="shutter-flash"></div>
        </div>
        <!-- scan line -->
        <div class="scan-line"></div>
      </div>

      <!-- hero content -->
      <div class="hero-content">
        <!-- Badge pill -->
        <div style="display:inline-flex;align-items:center;gap:8px;background:#fff;border:1px solid #e5e7eb;border-radius:999px;padding:8px 20px;font-size:13px;font-weight:600;color:#374151;margin-bottom:32px;box-shadow:0 2px 8px rgba(0,0,0,0.06);">
          <span>🎉</span>
          <span>#1 Marketplace for Video Creators</span>
        </div>

        <!-- Headline -->
        <h1 style="font-size:clamp(48px,8vw,88px);font-weight:900;line-height:0.95;letter-spacing:-2px;color:#111;text-transform:uppercase;margin:0 0 24px;">
          THE AI TOOLKIT <span style="color:#22c55e;">CREATORS</span><br/>ACTUALLY NEED
        </h1>

        <!-- Subtitle -->
        <p style="font-size:16px;color:#6b7280;margin:0 0 36px;font-weight:400;letter-spacing:0.1px;">
          With Built-In AI Models, Template Marketplace &amp; Plugin Support
        </p>

        <!-- CTA -->
        <a href="#" style="display:inline-block;background:#22c55e;color:#fff;font-size:16px;font-weight:700;padding:16px 48px;border-radius:999px;text-decoration:none;box-shadow:0 8px 24px rgba(34,197,94,0.35);transition:all 0.2s;margin-bottom:60px;">
          Browse Marketplace
        </a>
      </div>
    </section>

    <!-- ═══ POLAROID CARDS ON DEEP U-WIRE ═══ -->
    <!-- Desktop: absolute U-wire layout | Mobile: horizontal scroll snap carousel -->
    <section class="cards-section">

      <!-- ── Desktop wire + absolute cards ── -->
      <div class="cards-desktop">
        <!-- Wire SVG -->
        <svg
          style="position:absolute;top:0;left:0;width:100%;height:170px;pointer-events:none;z-index:1;"
          viewBox="0 0 1100 170"
          preserveAspectRatio="none"
        >
          <path d="M 0 10 Q 550 300 1100 10" fill="none" stroke="#9ca3af" stroke-width="1.8" />
        </svg>

        <!-- Cards pinned to wire points -->
        <div
          v-for="(card, i) in cards" :key="'d'+i"
          class="sway-card"
          :data-card-id="'d'+i"
          :style="{
            position:       'absolute',
            left:           ['7%', '25%', '44%', '63%', '81%'][i],
            top:            ['62px', '127px', '145px', '127px', '72px'][i],
            width:          '190px',
            zIndex:         touchedCard === 'd'+i ? 50 : 10,
            animationDelay: swayDelay[i],
          }"
          @mouseenter="(e) => { const v = (e.currentTarget as HTMLElement).querySelector('video'); if(v){ v.load(); v.play() } }"
          @mouseleave="(e) => { const v = (e.currentTarget as HTMLElement).querySelector('video'); if(v){ v.pause(); v.currentTime=0 } }"
          @touchstart.prevent="(e) => onCardTouch('d'+i, e.currentTarget as HTMLElement)"
        >
          <div style="display:flex;flex-direction:column;align-items:center;">
            <div style="width:14px;height:14px;background:#22c55e;border-radius:50%;border:2.5px solid #fff;box-shadow:0 2px 10px rgba(34,197,94,0.55);"></div>
            <div style="width:2px;height:16px;background:#22c55e;"></div>
          </div>
          <div class="polaroid" :class="{ 'card-touched': touchedCard === 'd'+i }" style="background:#fff;border-radius:14px;box-shadow:0 12px 40px rgba(0,0,0,0.13);overflow:hidden;">
            <div style="width:100%;height:155px;position:relative;overflow:hidden;">
              <iframe v-if="card.iframe" :src="card.iframe" frameborder="0" scrolling="no" style="width:100%;height:100%;border:none;display:block;"></iframe>
              <video v-else class="card-video" :src="card.video" muted loop playsinline preload="auto" style="width:100%;height:100%;object-fit:cover;display:block;"></video>
            </div>
            <div style="padding:12px 14px 14px;">
              <p style="font-size:13px;font-weight:700;color:#111;margin:0 0 3px;">{{ card.label }}</p>
              <p style="font-size:11px;color:#9ca3af;margin:0;line-height:1.4;">{{ card.sub }}</p>
            </div>
          </div>
        </div>

        <!-- Water droplets -->
        <div v-for="n in 20" :key="n" class="drop"
          :style="{ left:(n*4.8)+'%', width:(4+(n%4)*1.5)+'px', height:(7+(n%4)*2.5)+'px', animationDuration:(1.1+(n%5)*0.3)+'s', animationDelay:(n*0.22)+'s' }"
        ></div>
      </div>

      <!-- ── Mobile carousel ── -->
      <div class="cards-mobile">
        <!-- Single shared wire line across top -->
        <div class="mobile-wire"></div>
        <div class="cards-carousel">
          <div
            v-for="(card, i) in cards" :key="'m'+i"
            class="carousel-slide"
          >
            <!-- pin -->
            <div style="display:flex;flex-direction:column;align-items:center;">
              <div style="width:14px;height:14px;background:#22c55e;border-radius:50%;border:2.5px solid #fff;box-shadow:0 2px 10px rgba(34,197,94,0.55);"></div>
              <div style="width:2px;height:16px;background:#22c55e;"></div>
            </div>
            <!-- polaroid -->
            <div
              class="sway-card polaroid"
              :class="{ 'card-touched': touchedCard === 'm'+i }"
              :data-card-id="'m'+i"
              :style="{ animationDelay: swayDelay[i] }"
              style="background:#fff;border-radius:14px;box-shadow:0 12px 40px rgba(0,0,0,0.13);overflow:hidden;"
              @touchstart.prevent="(e) => onCardTouch('m'+i, e.currentTarget as HTMLElement)"
            >
              <div style="width:100%;height:155px;overflow:hidden;">
                <video :src="card.video" muted loop playsinline preload="auto" style="width:100%;height:100%;object-fit:cover;display:block;"></video>
              </div>
              <div style="padding:12px 14px 14px;">
                <p style="font-size:13px;font-weight:700;color:#111;margin:0 0 3px;">{{ card.label }}</p>
                <p style="font-size:11px;color:#9ca3af;margin:0;line-height:1.4;">{{ card.sub }}</p>
              </div>
            </div>
          </div>
        </div>
        <!-- scroll dots -->
        <div class="carousel-dots">
          <span v-for="(_, i) in cards" :key="i" class="carousel-dot"></span>
        </div>
      </div>

    </section>
    <section style="border-top:1px solid #e5e7eb;padding:28px 0;overflow:hidden;background:rgba(255,255,255,0.5);margin-top:20px;">
      <div style="display:flex;animation:ticker 24s linear infinite;width:max-content;">
        <div v-for="(logo, i) in logos" :key="i"
          style="display:flex;align-items:center;gap:8px;margin:0 40px;white-space:nowrap;color:#9ca3af;font-size:15px;font-weight:700;letter-spacing:-0.3px;">
          <span style="width:8px;height:8px;background:#d1d5db;border-radius:50%;display:inline-block;"></span>
          {{ logo }}
        </div>
      </div>
    </section>

    <!-- ═══ INTRO HOOK ═══ -->
    <section style="max-width:720px;margin:80px auto;padding:0 32px;text-align:center;">
      <p style="font-size:18px;color:#374151;line-height:1.8;margin:0 0 16px;">Now that you've enrolled in the <strong>AI Creator Course</strong>, you might be thinking...</p>
      <p style="font-size:22px;font-weight:700;color:#111;margin:0 0 16px;">Where is the best place to access the AI tools I'm going to learn about?</p>
      <p style="font-size:18px;color:#374151;line-height:1.8;margin:0 0 16px;">And just as important...</p>
      <p style="font-size:22px;font-weight:700;color:#111;margin:0 0 32px;">How can I save as much money as possible in the process?</p>
      <div style="background:#f0fdf4;border:2px solid #22c55e;border-radius:20px;padding:36px 40px;margin-bottom:32px;">
        <p style="font-size:20px;font-weight:700;color:#111;margin:0 0 12px;">Think of PromptEdit like a <span style="color:#22c55e;">grocery store for AI.</span></p>
        <p style="font-size:16px;color:#374151;line-height:1.8;margin:0;">Instead of signing up for a bunch of different websites, learning a bunch of different interfaces, and stacking expensive subscriptions on top of each other — PromptEdit gives you <strong>one place</strong> to access all the major tools you need to create AI content.</p>
      </div>
      <div class="intro-grid">
        <div style="background:#fff;border-radius:16px;padding:24px 16px;box-shadow:0 4px 20px rgba(0,0,0,0.06);border:1px solid #e5e7eb;">
          <div style="font-size:32px;margin-bottom:8px;">🚫</div>
          <p style="font-size:14px;font-weight:700;color:#111;margin:0 0 4px;">No Subscription Required</p>
          <p style="font-size:12px;color:#6b7280;margin:0;">Try the tools. Use the tools. Pay only for what you use.</p>
        </div>
        <div style="background:#fff;border-radius:16px;padding:24px 16px;box-shadow:0 4px 20px rgba(0,0,0,0.06);border:1px solid #e5e7eb;">
          <div style="font-size:32px;margin-bottom:8px;">⛽</div>
          <p style="font-size:14px;font-weight:700;color:#111;margin:0 0 4px;">AI Credits System</p>
          <p style="font-size:12px;color:#6b7280;margin:0;">Like buying gas for a car — purchase credits and use them on any tool.</p>
        </div>
        <div style="background:#fff;border-radius:16px;padding:24px 16px;box-shadow:0 4px 20px rgba(0,0,0,0.06);border:1px solid #e5e7eb;">
          <div style="font-size:32px;margin-bottom:8px;">💰</div>
          <p style="font-size:14px;font-weight:700;color:#111;margin:0 0 4px;">Exclusive Student Discount</p>
          <p style="font-size:12px;color:#6b7280;margin:0;">Special discounted credit offer for AI Creator Course students.</p>
        </div>
      </div>
    </section>

    <!-- ═══ INTRODUCING PROMPTEDIT ═══ -->
    <section style="background:#111;padding:80px 32px;text-align:center;">
      <p style="font-size:13px;font-weight:700;color:#22c55e;letter-spacing:3px;text-transform:uppercase;margin:0 0 16px;">Introducing</p>
      <h2 style="font-size:clamp(36px,6vw,64px);font-weight:900;color:#fff;margin:0 0 16px;letter-spacing:-1px;">Prompt Edit</h2>
      <p style="font-size:18px;color:rgba(255,255,255,0.6);max-width:600px;margin:0 auto 48px;">The most affordable AI marketplace featuring the best AI tools. Each one accessible <strong style="color:#22c55e;">WITHOUT</strong> the need for a subscription. Just pay as you go.</p>
      <p style="font-size:20px;font-weight:700;color:#fff;margin:0 0 48px;">Let's break down exactly what you can access with Prompt Edit... 👇</p>

      <!-- AI Tools Grid -->
      <div style="max-width:1000px;margin:0 auto;display:grid;grid-template-columns:repeat(auto-fit,minmax(280px,1fr));gap:24px;">

        <!-- Image Tools -->
        <div style="background:rgba(255,255,255,0.05);border:1px solid rgba(255,255,255,0.1);border-radius:20px;padding:32px;text-align:left;">
          <div style="font-size:36px;margin-bottom:12px;">🖼️</div>
          <h3 style="font-size:20px;font-weight:800;color:#fff;margin:0 0 8px;">AI Image Tools</h3>
          <p style="font-size:13px;color:rgba(255,255,255,0.5);margin:0 0 20px;">What can you do with these image tools?</p>
          <ul style="list-style:none;padding:0;margin:0;display:flex;flex-direction:column;gap:10px;">
            <li v-for="item in ['AI Clones','Social Media Posts','Graphic Design','Image Editing','Youtube Thumbnails','Online Ads']" :key="item"
              style="display:flex;align-items:center;gap:10px;font-size:14px;color:rgba(255,255,255,0.8);">
              <span style="width:20px;height:20px;background:#22c55e;border-radius:50%;display:flex;align-items:center;justify-content:center;flex-shrink:0;font-size:11px;">✓</span>
              {{ item }}
            </li>
          </ul>
        </div>

        <!-- Video Tools -->
        <div style="background:rgba(255,255,255,0.05);border:1px solid rgba(255,255,255,0.1);border-radius:20px;padding:32px;text-align:left;">
          <div style="font-size:36px;margin-bottom:12px;">🎬</div>
          <h3 style="font-size:20px;font-weight:800;color:#fff;margin:0 0 8px;">AI Video Tools</h3>
          <p style="font-size:13px;color:rgba(255,255,255,0.5);margin:0 0 20px;">What can you do with these video tools?</p>
          <ul style="list-style:none;padding:0;margin:0;display:flex;flex-direction:column;gap:10px;">
            <li v-for="item in ['Clone Videos','Visual Effects','Cinematic Films','Video Ads','Reels & TikToks','Youtube Videos']" :key="item"
              style="display:flex;align-items:center;gap:10px;font-size:14px;color:rgba(255,255,255,0.8);">
              <span style="width:20px;height:20px;background:#22c55e;border-radius:50%;display:flex;align-items:center;justify-content:center;flex-shrink:0;font-size:11px;">✓</span>
              {{ item }}
            </li>
          </ul>
        </div>

        <!-- Audio Tools -->
        <div style="background:rgba(255,255,255,0.05);border:1px solid rgba(255,255,255,0.1);border-radius:20px;padding:32px;text-align:left;">
          <div style="font-size:36px;margin-bottom:12px;">🎵</div>
          <h3 style="font-size:20px;font-weight:800;color:#fff;margin:0 0 8px;">AI Audio Tools</h3>
          <p style="font-size:13px;color:rgba(255,255,255,0.5);margin:0 0 20px;">What can you do with these audio tools?</p>
          <ul style="list-style:none;padding:0;margin:0;display:flex;flex-direction:column;gap:10px;">
            <li v-for="item in ['AI Voiceovers','AI Voice Clones','Voice Swaps','AI Sound Effects','AI Music Generation']" :key="item"
              style="display:flex;align-items:center;gap:10px;font-size:14px;color:rgba(255,255,255,0.8);">
              <span style="width:20px;height:20px;background:#22c55e;border-radius:50%;display:flex;align-items:center;justify-content:center;flex-shrink:0;font-size:11px;">✓</span>
              {{ item }}
            </li>
          </ul>
        </div>

        <!-- Editing Plugins -->
        <div style="background:rgba(34,197,94,0.1);border:1px solid rgba(34,197,94,0.3);border-radius:20px;padding:32px;text-align:left;">
          <div style="font-size:36px;margin-bottom:12px;">🔌</div>
          <h3 style="font-size:20px;font-weight:800;color:#fff;margin:0 0 8px;">AI Editing Plugins</h3>
          <p style="font-size:13px;color:rgba(255,255,255,0.5);margin:0 0 20px;">What can you do with these AI editing plugins?</p>
          <p style="font-size:14px;color:rgba(255,255,255,0.8);line-height:1.7;margin:0;">Access AI tools <strong style="color:#22c55e;">within your editing software.</strong> No need to open a browser window. The plugins open inside of your favorite editing software, allowing you to generate AI creations and instantly add them to any project.</p>
        </div>

      </div>
    </section>

    <!-- ═══ PRICING ═══ -->
    <section id="pricing" style="padding:80px 32px;background:#fafaf5;text-align:center;">
      <p style="font-size:13px;font-weight:700;color:#22c55e;letter-spacing:3px;text-transform:uppercase;margin:0 0 12px;">Prompt Edit Pricing</p>
      <h2 style="font-size:clamp(32px,5vw,52px);font-weight:900;color:#111;margin:0 0 16px;letter-spacing:-1px;">Existing Student Discount</h2>
      <p style="font-size:18px;color:#6b7280;margin:0 0 56px;">Save on Credits &amp; Unlock Everything</p>

      <div style="max-width:900px;margin:0 auto;display:grid;grid-template-columns:repeat(auto-fit,minmax(300px,1fr));gap:24px;">

        <!-- One-time plan -->
        <div style="background:#fff;border-radius:24px;padding:40px 32px;box-shadow:0 8px 40px rgba(0,0,0,0.08);border:2px solid #e5e7eb;text-align:left;">
          <p style="font-size:13px;font-weight:700;color:#6b7280;text-transform:uppercase;letter-spacing:2px;margin:0 0 12px;">One Payment</p>
          <div style="display:flex;align-items:baseline;gap:4px;margin-bottom:8px;">
            <span style="font-size:52px;font-weight:900;color:#111;">$98</span>
          </div>
          <p style="font-size:16px;font-weight:700;color:#22c55e;margin:0 0 20px;">Get $110 Worth of AI Credits Today</p>
          <p style="font-size:14px;color:#6b7280;margin:0 0 24px;line-height:1.6;">Save 10% when you claim offer. Use your credits on any AI tool across the entire site!</p>
          <p style="font-size:13px;color:#374151;margin:0 0 24px;font-style:italic;">Nano Banana Pro, Grok, Seedance, Kling, Veo, Heygen, Eleven Labs, Suno, Ideogram, and so many more!</p>
          <p style="font-size:13px;color:#6b7280;margin:0 0 28px;">If you run out of credits, simply purchase more — no subscriptions required.</p>
          <a href="#" style="display:block;text-align:center;background:#111;color:#fff;font-size:15px;font-weight:700;padding:16px;border-radius:12px;text-decoration:none;">Claim Credits Offer →</a>
        </div>

        <!-- Monthly plan -->
        <div style="background:#111;border-radius:24px;padding:40px 32px;box-shadow:0 8px 40px rgba(34,197,94,0.2);border:2px solid #22c55e;text-align:left;position:relative;overflow:hidden;">
          <div style="position:absolute;top:16px;right:16px;background:#22c55e;color:#fff;font-size:11px;font-weight:800;padding:4px 12px;border-radius:999px;">BEST VALUE</div>
          <p style="font-size:13px;font-weight:700;color:#22c55e;text-transform:uppercase;letter-spacing:2px;margin:0 0 12px;">Save on Everything</p>
          <div style="display:flex;align-items:baseline;gap:4px;margin-bottom:8px;">
            <span style="font-size:52px;font-weight:900;color:#fff;">$39</span>
            <span style="font-size:16px;color:rgba(255,255,255,0.5);">/month</span>
          </div>
          <p style="font-size:16px;font-weight:700;color:#22c55e;margin:0 0 20px;">Get $49 Worth of AI Credits every month + 10% off anytime you purchase more</p>
          <ul style="list-style:none;padding:0;margin:0 0 28px;display:flex;flex-direction:column;gap:10px;">
            <li v-for="feat in ['Lifetime 20% boost on monthly credits','10% off additional credit purchases','Unlimited Content Creator Templates Library','Faster generation speeds','Run multiple generations at once','Easily cancel at any time']" :key="feat"
              style="display:flex;align-items:center;gap:10px;font-size:14px;color:rgba(255,255,255,0.8);">
              <span style="color:#22c55e;font-size:16px;">✓</span> {{ feat }}
            </li>
          </ul>
          <a href="#" style="display:block;text-align:center;background:#22c55e;color:#fff;font-size:15px;font-weight:700;padding:16px;border-radius:12px;text-decoration:none;">Start Monthly Plan →</a>
        </div>

      </div>
    </section>

    <!-- ═══ TEMPLATES LIBRARY ═══ -->
    <section style="padding:80px 32px;background:#fff;text-align:center;">
      <p style="font-size:13px;font-weight:700;color:#22c55e;letter-spacing:3px;text-transform:uppercase;margin:0 0 12px;">Included with Monthly Subscription</p>
      <h2 style="font-size:clamp(28px,5vw,48px);font-weight:900;color:#111;margin:0 0 16px;letter-spacing:-1px;">Content Creator Templates Library</h2>
      <p style="font-size:16px;color:#6b7280;max-width:680px;margin:0 auto 56px;line-height:1.7;">Over <strong>100,000+</strong> professionally designed editing templates &amp; packs that will drastically improve the look and feel of your videos while saving you countless hours.</p>

      <div style="max-width:1100px;margin:0 auto;display:grid;grid-template-columns:repeat(auto-fit,minmax(260px,1fr));gap:20px;">
        <div v-for="cat in [
          { icon:'🎨', count:'4,000+', name:'LUTs', desc:'Drag and drop color presets that give your videos a cinematic look in seconds. Works with any editing software.' },
          { icon:'🔊', count:'60,000+', name:'Sound Effects', desc:'Professionally made SFX for every situation. Drag and drop into any editing software.' },
          { icon:'💬', count:'3,000+', name:'Text Animations', desc:'Scroll-stopping text templates. Pick a layout, type your message, and watch your ideas come to life.' },
          { icon:'🪄', count:'2,000+', name:'Overlays', desc:'Viral social media looks and vintage vibes. Just drag, change blend mode, and boom — new style.' },
          { icon:'✅', count:'5,000+', name:'Backgrounds', desc:'Clean, professional animated backgrounds. Add images or text on top for a polished result.' },
        ]" :key="cat.name"
          style="background:#f8f7ff;border-radius:20px;padding:28px 24px;text-align:left;border:1px solid #e5e7eb;">
          <div style="font-size:36px;margin-bottom:10px;">{{ cat.icon }}</div>
          <div style="display:flex;align-items:baseline;gap:6px;margin-bottom:6px;">
            <span style="font-size:28px;font-weight:900;color:#22c55e;">{{ cat.count }}</span>
            <span style="font-size:16px;font-weight:700;color:#111;">{{ cat.name }}</span>
          </div>
          <p style="font-size:13px;color:#6b7280;margin:0;line-height:1.6;">{{ cat.desc }}</p>
        </div>
      </div>
    </section>

    <!-- ═══ TESTIMONIALS ═══ -->
    <section style="padding:80px 32px;background:#f8f7ff;text-align:center;">
      <h2 style="font-size:clamp(28px,4vw,42px);font-weight:900;color:#111;margin:0 0 48px;letter-spacing:-0.5px;">What Creators Are Saying</h2>
      <div style="max-width:1000px;margin:0 auto;display:grid;grid-template-columns:repeat(auto-fit,minmax(280px,1fr));gap:24px;">
        <div v-for="t in [
          { quote: 'My daughter and I got more editing work done today in 3 hours than we normally do in 3 days!', name: 'Hilda Schlueter', role: 'Online Course Creator' },
          { quote: 'My videos wouldn\'t look HALF as good as they do if it wasn\'t for the Content Creator Templates Library. I lean into them heavily for every edit I do.', name: 'Matt Lilley', role: 'ContentCreator.com Student' },
          { quote: 'The Content Creator Templates Library is a fantastic resource! I don\'t need any other digital asset subscriptions.', name: 'Brady Hales', role: 'ContentCreator.com Student' },
        ]" :key="t.name"
          style="background:#fff;border-radius:20px;padding:28px;box-shadow:0 4px 20px rgba(0,0,0,0.06);border:1px solid #e5e7eb;text-align:left;">
          <div style="color:#f59e0b;font-size:18px;margin-bottom:12px;">★★★★★</div>
          <p style="font-size:15px;color:#374151;line-height:1.7;margin:0 0 20px;font-style:italic;">"{{ t.quote }}"</p>
          <div>
            <p style="font-size:14px;font-weight:700;color:#111;margin:0;">— {{ t.name }}</p>
            <p style="font-size:12px;color:#9ca3af;margin:4px 0 0;">{{ t.role }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- ═══ IS THIS FOR YOU ═══ -->
    <section style="padding:80px 32px;background:#fff;max-width:800px;margin:0 auto;">
      <h2 style="font-size:clamp(28px,4vw,42px);font-weight:900;color:#111;margin:0 0 12px;text-align:center;">A Subscription to PromptEdit.com is for you if...</h2>
      <p style="text-align:center;color:#6b7280;margin:0 0 40px;">Including the Content Creator Templates Library</p>
      <ul style="list-style:none;padding:0;margin:0 0 48px;display:flex;flex-direction:column;gap:16px;">
        <li v-for="item in [
          'You want to access all of the best AI tools in one place, with an easy to use interface',
          'You want the best deal on AI credits, allowing you to CREATE more and SAVE more money',
          'You want to produce cinematic videos using the same time-saving templates professional editors in Hollywood use',
          'You just started learning how to edit but still want to get that professional look without spending months figuring out how to build everything yourself',
          'You\'re tired of searching the internet endlessly, looking for that one perfect template, only to find you need to buy a pack that costs $130',
          'You care about UNLIMITED Downloads & UNLIMITED Usage',
        ]" :key="item"
          style="display:flex;align-items:flex-start;gap:14px;padding:16px 20px;background:#f0fdf4;border-radius:12px;border:1px solid #bbf7d0;">
          <span style="width:24px;height:24px;background:#22c55e;border-radius:50%;display:flex;align-items:center;justify-content:center;color:#fff;font-size:13px;font-weight:700;flex-shrink:0;margin-top:1px;">✓</span>
          <span style="font-size:15px;color:#374151;line-height:1.6;">{{ item }}</span>
        </li>
      </ul>
      <div style="background:#111;border-radius:20px;padding:32px;text-align:center;">
        <p style="font-size:20px;font-weight:800;color:#fff;margin:0 0 8px;">🛡️ 100% Money Back Guarantee</p>
        <p style="font-size:14px;color:rgba(255,255,255,0.6);margin:0 0 24px;line-height:1.6;">Cancel your subscription any time. Within 30 days of purchase you can get a full refund on unused credits. No catch, no questions asked.</p>
        <a href="#pricing" style="display:inline-block;background:#22c55e;color:#fff;font-size:16px;font-weight:700;padding:16px 48px;border-radius:999px;text-decoration:none;">Get Started Today →</a>
      </div>
    </section>

    <!-- ═══ FAQ ═══ -->
    <section style="padding:80px 32px;background:#f8f7ff;max-width:800px;margin:0 auto;">
      <h2 style="font-size:clamp(28px,4vw,42px);font-weight:900;color:#111;margin:0 0 40px;text-align:center;">Commonly Asked Questions</h2>
      <div style="display:flex;flex-direction:column;gap:12px;">
        <details v-for="faq in [
          { q: 'What is PromptEdit.com?', a: 'PromptEdit is an AI marketplace that gives you access to all the major AI tools in one place — no subscriptions required. Just purchase credits and use them on any tool.' },
          { q: 'Can I use what I create for social media or commercial videos?', a: 'Yes! Everything you create using PromptEdit tools can be used for personal and commercial projects.' },
          { q: 'Is there a difference in quality between AI tools on PromptEdit.com and the same tool on the company\'s main website?', a: 'No. You get access to the exact same models and quality. PromptEdit simply provides a unified, affordable interface.' },
          { q: 'What is Content Creator Templates?', a: 'It\'s a library of 100,000+ professionally designed editing templates including LUTs, SFX, text animations, overlays, and backgrounds — included with your monthly subscription.' },
          { q: 'Do any limits apply to downloads?', a: 'No limits. Unlimited downloads and unlimited usage are included with your subscription.' },
          { q: 'Will the templates work in my editing platform?', a: 'Yes. Our templates work with DaVinci Resolve, Adobe Premiere Pro, Final Cut Pro, and all major editing software.' },
          { q: 'Can I cancel at anytime?', a: 'Absolutely. Cancel anytime with no penalties. Within 30 days you can also request a full refund on unused credits.' },
          { q: 'What happens to the templates I\'ve downloaded if I cancel?', a: 'Any templates you\'ve already downloaded are yours to keep and use forever.' },
        ]" :key="faq.q"
          style="background:#fff;border-radius:14px;border:1px solid #e5e7eb;overflow:hidden;">
          <summary style="padding:20px 24px;font-size:15px;font-weight:700;color:#111;cursor:pointer;list-style:none;display:flex;justify-content:space-between;align-items:center;">
            {{ faq.q }}
            <span style="color:#22c55e;font-size:20px;flex-shrink:0;">+</span>
          </summary>
          <p style="padding:0 24px 20px;font-size:14px;color:#6b7280;margin:0;line-height:1.7;">{{ faq.a }}</p>
        </details>
      </div>
    </section>

    <!-- ═══ FOOTER ═══ -->
    <footer style="background:#111;padding:48px 32px;text-align:center;">
      <p style="font-size:20px;font-weight:900;color:#fff;margin:0 0 8px;">PromptEdit<span style="color:#22c55e;">.</span></p>
      <p style="font-size:13px;color:rgba(255,255,255,0.4);margin:0 0 24px;">© 2025 Paul Xavier International LLC</p>
      <p style="font-size:12px;color:rgba(255,255,255,0.3);max-width:700px;margin:0 auto 16px;line-height:1.6;">By visiting this page, you agree to terms and conditions, privacy policy &amp; earnings disclaimer. This site is not a part of the Facebook website or Facebook Inc.</p>
      <p style="font-size:11px;color:rgba(255,255,255,0.2);max-width:700px;margin:0 auto;line-height:1.6;">DISCLAIMER: The sales figures stated on this landing page are our personal sales figures and in some cases the sales figures of previous or existing clients. Results are not typical. Your results will vary and depend on many factors including your background, experience, and work ethic.</p>
    </footer>

  </div>
</template>

<style scoped>
@keyframes ticker {
  0%   { transform: translateX(0); }
  100% { transform: translateX(-50%); }
}

/* Wind sway — pivots from pin at top */
@keyframes sway {
  0%   { transform: rotate(-5deg); }
  25%  { transform: rotate(5deg);  }
  50%  { transform: rotate(-4deg); }
  75%  { transform: rotate(4deg);  }
  100% { transform: rotate(-5deg); }
}
.sway-card {
  animation: sway 3.2s ease-in-out infinite;
  transform-origin: 50% 0% !important;
}
/* Pause sway + zoom in on hover */
.sway-card:hover {
  animation-play-state: paused;
  z-index: 50 !important;
}
.sway-card:hover :deep(.polaroid) {
  transform: scale(1.12);
  box-shadow: 0 24px 60px rgba(0,0,0,0.22);
  transition: transform 0.35s cubic-bezier(.34,1.56,.64,1), box-shadow 0.35s ease;
}
.polaroid {
  transition: transform 0.35s ease, box-shadow 0.35s ease;
}
.card-touched {
  transform: scale(1.12);
  box-shadow: 0 24px 60px rgba(0,0,0,0.22) !important;
  transition: transform 0.35s cubic-bezier(.34,1.56,.64,1), box-shadow 0.35s ease;
}

/* Water droplets */
@keyframes fall {
  0%   { transform: translateY(0);     opacity: 0.8; }
  100% { transform: translateY(100px); opacity: 0;   }
}
.drop {
  position: absolute;
  bottom: 0;
  border-radius: 50% 50% 50% 50% / 35% 35% 65% 65%;
  background: linear-gradient(180deg, rgba(96,165,250,0.8), rgba(59,130,246,0.25));
  animation: fall linear infinite;
  pointer-events: none;
  z-index: 5;
}

a[href="#"]:last-of-type:hover {
  background: #16a34a;
}

/* ── Header shell ── */
.site-header {
  position: sticky;
  top: 0;
  z-index: 100;
  background: #fff;
  box-shadow: 0 1px 0 #e5e7eb;
}

/* ── Top utility bar ── */
.nav-top {
  background: #111;
  padding: 0 32px;
}
.nav-top-inner {
  max-width: 1280px;
  margin: 0 auto;
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 36px;
}
.nav-top-left, .nav-top-right {
  display: flex;
  align-items: center;
  gap: 20px;
}
.nav-top a {
  font-size: 12px;
  color: rgba(255,255,255,0.65);
  text-decoration: none;
  font-weight: 500;
  transition: color 0.15s;
}
.nav-top a:hover { color: #fff; }
.nav-login {
  color: rgba(255,255,255,0.8) !important;
}
.nav-signup {
  background: rgba(255,255,255,0.12);
  color: #fff !important;
  padding: 4px 14px;
  border-radius: 999px;
  border: 1px solid rgba(255,255,255,0.2);
}
.nav-signup:hover { background: rgba(255,255,255,0.2) !important; }
.nav-unlimited {
  background: #22c55e !important;
  color: #fff !important;
  padding: 4px 14px;
  border-radius: 999px;
  font-weight: 700 !important;
}
.nav-unlimited:hover { background: #16a34a !important; }

/* ── Main nav ── */
.nav-main {
  max-width: 1280px;
  margin: 0 auto;
  padding: 0 32px;
  display: flex;
  align-items: center;
  gap: 20px;
  height: 56px;
}
.nav-logo {
  font-size: 18px;
  font-weight: 900;
  color: #111;
  text-decoration: none;
  letter-spacing: -0.5px;
  white-space: nowrap;
  display: flex;
  align-items: center;
  gap: 5px;
  flex-shrink: 0;
}
.logo-dot { color: #22c55e; font-size: 10px; }

/* Search bar */
.nav-search-bar {
  display: flex;
  align-items: center;
  gap: 8px;
  background: #f3f4f6;
  border: 1px solid #e5e7eb;
  border-radius: 999px;
  padding: 7px 16px;
  flex: 0 1 280px;
  color: #9ca3af;
}
.nav-search-bar input {
  border: none;
  background: transparent;
  outline: none;
  font-size: 13px;
  color: #374151;
  width: 100%;
}
.nav-search-bar input::placeholder { color: #9ca3af; }

/* Category links */
.nav-links {
  display: flex;
  align-items: center;
  gap: 2px;
  overflow-x: auto;
  scrollbar-width: none;
  flex: 1;
}
.nav-links::-webkit-scrollbar { display: none; }
.nav-link {
  font-size: 13px;
  font-weight: 500;
  color: #374151;
  text-decoration: none;
  padding: 6px 10px;
  border-radius: 8px;
  white-space: nowrap;
  transition: background 0.15s, color 0.15s;
}
.nav-link:hover {
  background: #f3f4f6;
  color: #111;
}
.nav-link-ai {
  color: #7c3aed;
  font-weight: 700;
  background: #f5f3ff;
}
.nav-link-ai:hover {
  background: #ede9fe;
  color: #6d28d9;
}

/* ── Gen AI Dropdown ── */
.nav-link-ai {
  border: none;
  cursor: pointer;
}
.ai-chevron {
  font-size: 10px;
  margin-left: 2px;
  opacity: 0.7;
  display: inline-block;
  transition: transform 0.2s;
}
.ai-chevron.open { transform: rotate(180deg); }
.ai-dropdown-panel {
  position: absolute;
  top: 100%;
  left: 0;
  right: 0;
  background: #fff;
  border-top: 1px solid #e5e7eb;
  border-bottom: 1px solid #e5e7eb;
  box-shadow: 0 8px 32px rgba(0,0,0,0.10);
  padding: 12px 32px;
  z-index: 300;
  display: flex;
  align-items: flex-start;
  gap: 4px;
  overflow-x: auto;
  scrollbar-width: none;
}
.ai-dropdown-panel::-webkit-scrollbar { display: none; }
.ai-dropdown-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  gap: 6px;
  padding: 14px 16px;
  border-radius: 12px;
  text-decoration: none;
  transition: background 0.15s;
  flex: 1;
  min-width: 100px;
}
.ai-dropdown-item:hover { background: #f5f3ff; }
.ai-item-emoji {
  font-size: 26px;
  flex-shrink: 0;
}
.ai-item-name {
  font-size: 13px;
  font-weight: 700;
  color: #111;
  margin: 0;
  white-space: nowrap;
}
.ai-item-desc {
  font-size: 11px;
  color: #6b7280;
  margin: 0;
  line-height: 1.4;
  white-space: normal;
}

/* ── Hamburger ── */
.nav-hamburger {
  display: none;
  flex-direction: column;
  justify-content: center;
  gap: 5px;
  background: none;
  border: none;
  cursor: pointer;
  padding: 6px;
  margin-left: auto;
  width: 36px;
  height: 36px;
}
.nav-hamburger span {
  display: block;
  width: 22px;
  height: 2px;
  background: #111;
  border-radius: 2px;
  transition: transform 0.35s cubic-bezier(.77,0,.18,1), opacity 0.2s;
  transform-origin: center;
}
/* bar 1 & 3 rotate into X */
.bar-open:first-child  { transform: translateY(7px) rotate(45deg); }
.bar-open:last-child   { transform: translateY(-7px) rotate(-45deg); }
/* middle bar fades out */
.bar-open-mid          { opacity: 0; transform: scaleX(0); }

/* ── Mobile menu ── */
.mobile-menu {
  background: #0f0f0f;
  border-top: 1px solid rgba(255,255,255,0.08);
  overflow: hidden;
}

/* slide transition */
.menu-slide-enter-active,
.menu-slide-leave-active {
  transition: max-height 0.4s cubic-bezier(.77,0,.18,1), opacity 0.3s ease;
  max-height: 800px;
}
.menu-slide-enter-from,
.menu-slide-leave-to {
  max-height: 0;
  opacity: 0;
}

/* submenu slide */
.submenu-slide-enter-active,
.submenu-slide-leave-active {
  transition: max-height 0.3s ease, opacity 0.25s ease;
  max-height: 600px;
  overflow: hidden;
}
.submenu-slide-enter-from,
.submenu-slide-leave-to {
  max-height: 0;
  opacity: 0;
}

/* utility row */
.mm-utility {
  display: flex;
  gap: 8px;
  padding: 16px 20px 12px;
  border-bottom: 1px solid rgba(255,255,255,0.07);
}
.mm-util-link {
  font-size: 12px;
  font-weight: 600;
  color: rgba(255,255,255,0.5);
  text-decoration: none;
  padding: 5px 12px;
  border-radius: 999px;
  border: 1px solid rgba(255,255,255,0.12);
  transition: color 0.15s, border-color 0.15s;
}
.mm-util-link:hover { color: #fff; border-color: rgba(255,255,255,0.3); }

/* nav links */
.mm-nav-links {
  display: flex;
  flex-direction: column;
  padding: 8px 0;
  border-bottom: 1px solid rgba(255,255,255,0.07);
}
.mm-link {
  font-size: 15px;
  font-weight: 500;
  color: rgba(255,255,255,0.75);
  text-decoration: none;
  padding: 13px 20px;
  transition: background 0.15s, color 0.15s;
  display: block;
}
.mm-link:hover { background: rgba(255,255,255,0.05); color: #fff; }

/* Gen AI toggle */
.mm-ai-toggle {
  width: 100%;
  background: none;
  border: none;
  cursor: pointer;
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-family: inherit;
  padding: 13px 20px;
  transition: background 0.15s;
}
.mm-ai-toggle:hover { background: rgba(255,255,255,0.05); }
.mm-ai-label {
  font-size: 15px;
  font-weight: 700;
  color: #a78bfa;
  display: flex;
  align-items: center;
  gap: 6px;
}
.mm-ai-star {
  font-size: 12px;
  color: #a78bfa;
}
.mm-ai-toggle .ai-chevron { color: #a78bfa; }

/* AI submenu on dark bg */
.mobile-ai-submenu {
  background: rgba(124,58,237,0.08);
  border-top: 1px solid rgba(124,58,237,0.15);
  border-bottom: 1px solid rgba(124,58,237,0.15);
}
.mobile-ai-item {
  display: flex;
  align-items: flex-start;
  gap: 12px;
  padding: 12px 32px;
  text-decoration: none;
  transition: background 0.15s;
}
.mobile-ai-item:hover { background: rgba(124,58,237,0.12); }
.mobile-ai-emoji { font-size: 22px; flex-shrink: 0; margin-top: 2px; }
.mobile-ai-item .ai-item-name { color: #fff; }
.mobile-ai-item .ai-item-desc { color: rgba(255,255,255,0.45); }

/* auth buttons */
.mm-auth {
  display: flex;
  gap: 10px;
  padding: 16px 20px;
  border-bottom: 1px solid rgba(255,255,255,0.07);
}
.mm-login {
  flex: 1;
  text-align: center;
  font-size: 14px;
  font-weight: 600;
  color: rgba(255,255,255,0.8);
  text-decoration: none;
  padding: 12px;
  border-radius: 12px;
  border: 1px solid rgba(255,255,255,0.15);
  transition: background 0.15s, color 0.15s;
}
.mm-login:hover { background: rgba(255,255,255,0.08); color: #fff; }
.mm-signup {
  flex: 1;
  text-align: center;
  font-size: 14px;
  font-weight: 700;
  color: #111;
  background: #fff;
  text-decoration: none;
  padding: 12px;
  border-radius: 12px;
  transition: background 0.15s;
}
.mm-signup:hover { background: #e5e7eb; }

/* CTA */
.mm-cta-wrap {
  padding: 16px 20px 20px;
}
.mm-cta {
  display: block;
  text-align: center;
  font-size: 15px;
  font-weight: 800;
  color: #fff;
  background: linear-gradient(135deg, #22c55e 0%, #16a34a 100%);
  text-decoration: none;
  padding: 16px;
  border-radius: 14px;
  box-shadow: 0 4px 24px rgba(34,197,94,0.4);
  letter-spacing: 0.2px;
  transition: box-shadow 0.2s, transform 0.2s;
}
.mm-cta:hover {
  box-shadow: 0 8px 32px rgba(34,197,94,0.55);
  transform: translateY(-1px);
}

@media (max-width: 768px) {
  .nav-hamburger { display: flex; }
  .nav-search-bar { display: none; }
  .nav-links { display: none; }
  .nav-top { display: none; }
}

/* ── Cards section layout ── */
.cards-section {
  margin-bottom: 40px;
}
.cards-desktop {
  position: relative;
  width: 100%;
  height: 460px;
  overflow: visible;
}
.cards-mobile {
  display: none;
  flex-direction: column;
  align-items: center;
  padding: 0 0 24px;
  position: relative;
}
.mobile-wire {
  width: 100%;
  height: 2px;
  background: linear-gradient(90deg, transparent 0%, #9ca3af 10%, #9ca3af 90%, transparent 100%);
  margin-bottom: 0;
  position: absolute;
  top: 14px;
  left: 0;
}
.cards-carousel {
  display: flex;
  overflow-x: scroll;
  scroll-snap-type: x mandatory;
  -webkit-overflow-scrolling: touch;
  scrollbar-width: none;
  gap: 20px;
  padding: 0 32px 16px;
  width: 100%;
  box-sizing: border-box;
}
.cards-carousel::-webkit-scrollbar { display: none; }
.carousel-slide {
  scroll-snap-align: center;
  flex-shrink: 0;
  width: 200px;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.carousel-dots {
  display: flex;
  gap: 6px;
  margin-top: 4px;
}
.carousel-dot {
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: #d1d5db;
}

.intro-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 16px;
  margin-bottom: 40px;
}

@media (max-width: 768px) {
  .cards-desktop { display: none; }
  .cards-mobile { display: flex; }
  .intro-grid { grid-template-columns: 1fr; }
}

/* ═══ HERO SECTION ═══ */
.hero-section {
  position: relative;
  text-align: center;
  padding: 40px 32px 0;
  max-width: 900px;
  margin: 0 auto;
  overflow: hidden;
}
.hero-content { position: relative; z-index: 2; }

/* hide on desktop */
.mobile-hero-bg { display: none; }

@media (max-width: 768px) {
  .mobile-hero-bg {
    display: block;
    position: absolute;
    inset: 0;
    z-index: 0;
    pointer-events: none;
    overflow: hidden;
  }

  /* ── Colour orbs ── */
  @keyframes bloom {
    0%   { transform: scale(0) translate(0,0); opacity: 0; }
    40%  { opacity: 0.55; }
    100% { transform: scale(1) translate(var(--tx), var(--ty)); opacity: 0.18; }
  }
  @keyframes drift {
    0%,100% { transform: scale(1)   translate(var(--tx), var(--ty)); }
    50%      { transform: scale(1.15) translate(calc(var(--tx) + 12px), calc(var(--ty) - 10px)); }
  }
  .orb {
    position: absolute;
    border-radius: 50%;
    animation: bloom 1.4s cubic-bezier(.22,1,.36,1) forwards, drift 6s ease-in-out infinite;
    animation-delay: var(--d), calc(var(--d) + 1.4s);
    filter: blur(32px);
  }
  .orb-1 { width:220px; height:220px; background:#22c55e; top:-40px; left:-60px; --tx:-10px; --ty:20px; --d:0s; }
  .orb-2 { width:180px; height:180px; background:#a78bfa; top:20px;  right:-50px; --tx:10px; --ty:30px; --d:0.2s; }
  .orb-3 { width:160px; height:160px; background:#f472b6; bottom:40px; left:10px;  --tx:-15px; --ty:-10px; --d:0.4s; }
  .orb-4 { width:140px; height:140px; background:#fbbf24; bottom:20px; right:20px; --tx:8px; --ty:-20px; --d:0.6s; }

  /* ── Light rays ── */
  @keyframes ray-in {
    0%   { opacity: 0; transform: scaleY(0) rotate(var(--r)); transform-origin: top center; }
    100% { opacity: 0.12; transform: scaleY(1) rotate(var(--r)); transform-origin: top center; }
  }
  .ray {
    position: absolute;
    top: 0;
    left: 50%;
    width: 3px;
    height: 100%;
    background: linear-gradient(180deg, rgba(255,255,255,0.9) 0%, transparent 100%);
    transform-origin: top center;
    animation: ray-in 1.8s ease forwards;
    animation-delay: var(--d);
  }
  .ray-1 { --r: -25deg; --d: 0.5s; }
  .ray-2 { --r:   0deg; --d: 0.7s; }
  .ray-3 { --r:  25deg; --d: 0.9s; }

  /* ── Sparkles ── */
  @keyframes sparkle {
    0%,100% { opacity: 0; transform: scale(0) translate(0,0); }
    50%      { opacity: 1; transform: scale(1) translate(var(--sx), var(--sy)); }
  }
  .spark {
    position: absolute;
    width: 8px;
    height: 8px;
    border-radius: 50%;
    background: #fff;
    animation: sparkle var(--dur) ease-in-out infinite;
    animation-delay: var(--d);
  }
  .spark-1 { top:18%; left:15%; --sx:6px;  --sy:-8px;  --dur:2.2s; --d:0.3s; }
  .spark-2 { top:12%; right:20%; --sx:-5px; --sy:6px;   --dur:2.8s; --d:0.8s; }
  .spark-3 { top:55%; left:8%;  --sx:8px;  --sy:-4px;  --dur:2.4s; --d:1.1s; }
  .spark-4 { top:65%; right:12%; --sx:-6px; --sy:-8px;  --dur:3.0s; --d:0.5s; }
  .spark-5 { top:35%; left:50%; --sx:4px;  --sy:10px;  --dur:2.6s; --d:1.4s; }

  /* ── Camera ── */
  @keyframes cam-enter {
    0%   { opacity: 0; transform: scale(0.4) translateY(30px); }
    60%  { opacity: 1; transform: scale(1.08) translateY(-6px); }
    100% { opacity: 1; transform: scale(1) translateY(0); }
  }
  @keyframes cam-float {
    0%,100% { transform: translateY(0) rotate(-2deg); }
    50%      { transform: translateY(-10px) rotate(2deg); }
  }
  @keyframes cam-glow {
    0%,100% { filter: drop-shadow(0 0 8px rgba(34,197,94,0.5)); }
    50%      { filter: drop-shadow(0 0 22px rgba(34,197,94,0.9)); }
  }
  @keyframes shutter {
    0%,90%,100% { opacity: 0; }
    92%          { opacity: 0.85; }
    96%          { opacity: 0; }
  }
  .cam-wrap {
    position: absolute;
    bottom: 24px;
    right: 24px;
    width: 110px;
    animation: cam-enter 1s cubic-bezier(.34,1.56,.64,1) 0.6s both,
               cam-float 4s ease-in-out 1.6s infinite,
               cam-glow  3s ease-in-out 1.6s infinite;
  }
  .cam-svg { width: 100%; display: block; }
  .shutter-flash {
    position: absolute;
    inset: 0;
    background: #fff;
    border-radius: 10px;
    animation: shutter 4s ease-in-out 2s infinite;
    pointer-events: none;
  }

  /* ── Scan line ── */
  @keyframes scan {
    0%   { top: 0%;   opacity: 0.6; }
    100% { top: 100%; opacity: 0; }
  }
  .scan-line {
    position: absolute;
    left: 0; right: 0;
    height: 2px;
    background: linear-gradient(90deg, transparent, rgba(34,197,94,0.7), transparent);
    animation: scan 3s linear 1.5s infinite;
  }
}
</style>
