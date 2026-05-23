<script setup lang="ts">
const cards = [
  { label: 'AI Prompts',    sub: 'Generate prompts for any AI model',  emoji: '⚡', bg: '#f472b6', rotate: '-6deg',  top: '0px'  },
  { label: 'Veo 3',         sub: 'Cinematic AI video generations',      emoji: '🎬', bg: '#a3e635', rotate: '-3deg',  top: '0px'   },
  { label: 'Templates',     sub: 'DaVinci & Premiere Pro packs',        emoji: '🎞️', bg: '#22d3ee', rotate: '0deg',   top: '-12px' },
  { label: 'KlingAI',       sub: 'Ready-to-use prompt bundles',         emoji: '🤖', bg: '#fb923c', rotate: '3deg',   top: '0px'   },
  { label: 'Geography',     sub: 'Sell your work worldwide',            emoji: '🌍', bg: '#1e293b', rotate: '6deg',   top: '18px'  },
]

const logos = ['promptedit', 'LIIIII', 'contentcreator', 'oop', 'Logoipsum', 'LOC', 'promptedit', 'LIIIII', 'contentcreator', 'oop', 'Logoipsum', 'LOC']
</script>

<template>
  <div style="min-height:100vh;background:radial-gradient(ellipse at 50% 0%,#e8f5e9 0%,#f5f5e8 40%,#fafaf5 100%);font-family:'Inter',sans-serif;overflow-x:hidden;">

    <!-- ═══ NAV ═══ -->
    <nav style="max-width:1100px;margin:0 auto;padding:22px 32px;display:flex;align-items:center;justify-content:space-between;">

      <!-- Logo -->
      <a href="#" style="text-decoration:none;display:flex;align-items:center;gap:1px;">
        <span style="font-size:20px;font-weight:900;color:#111;letter-spacing:-0.5px;">
          <span style="color:#111;">.A</span><span style="font-style:italic;color:#111;">s</span><span style="color:#111;">TR</span><span style="font-size:14px;vertical-align:super;color:#22c55e;">o</span>
        </span>
        <span style="font-size:20px;font-weight:900;color:#111;letter-spacing:-0.5px;margin-left:1px;">PromptEdit</span>
      </a>

      <!-- Center links -->
      <div style="display:flex;align-items:center;gap:36px;">
        <a href="#" style="font-size:14px;color:#374151;text-decoration:none;font-weight:500;">AI Tools</a>
        <a href="#" style="font-size:14px;color:#374151;text-decoration:none;font-weight:500;">Creator Portal</a>
        <a href="#" style="font-size:14px;color:#374151;text-decoration:none;font-weight:500;">Marketplace</a>
      </div>

      <!-- Right -->
      <div style="display:flex;align-items:center;gap:20px;">
        <a href="#" style="font-size:14px;color:#374151;text-decoration:none;font-weight:500;">Login</a>
        <a href="#" style="background:#22c55e;color:#fff;font-size:14px;font-weight:700;padding:11px 26px;border-radius:999px;text-decoration:none;transition:all 0.2s;">Get Started</a>
      </div>
    </nav>

    <!-- ═══ HERO ═══ -->
    <section style="text-align:center;padding:40px 32px 0;max-width:900px;margin:0 auto;">

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
    </section>

    <!-- ═══ POLAROID CARDS ON DEEP U-WIRE ═══ -->
    <!--
      Wire: Q bezier P0=(0,10) control=(550,300) P2=(1100,10)
      Deep U — 290px drop from edges to center.
      B(t)y = (1-t)²·10 + 2(1-t)t·300 + t²·10
        t=0.10 → y≈ 63px
        t=0.28 → y≈163px
        t=0.50 → y≈155px  (actual peak of parabola at t=0.5 → 155px)
      Recomputed:
        t=0.10: y=(0.81)(10)+2(0.9)(0.1)(300)+(0.01)(10) = 8.1+54+0.1 = 62px
        t=0.28: y=(0.5184)(10)+2(0.72)(0.28)(300)+(0.0784)(10)=5.18+120.96+0.78=127px
        t=0.50: y=(0.25)(10)+2(0.5)(0.5)(300)+(0.25)(10)=2.5+150+2.5=155px
        t=0.72: y=127px (symmetric)
        t=0.90: y=62px  (symmetric)
    -->
    <section style="position:relative;width:100%;height:460px;overflow:visible;margin-bottom:40px;">

      <!-- Wire SVG -->
      <svg
        style="position:absolute;top:0;left:0;width:100%;height:170px;pointer-events:none;z-index:1;"
        viewBox="0 0 1100 170"
        preserveAspectRatio="none"
      >
        <path
          d="M 0 10 Q 550 300 1100 10"
          fill="none"
          stroke="#9ca3af"
          stroke-width="1.8"
        />
      </svg>

      <!-- Cards pinned to wire points -->
      <div
        v-for="(card, i) in cards" :key="i"
        :style="{
          position:  'absolute',
          left:      ['7%', '25%', '44%', '63%', '81%'][i],
          top:       ['62px', '127px', '145px', '127px', '72px'][i],
          transform: `rotate(${card.rotate})`,
          width:     '190px',
          zIndex:    10,
        }"
      >
        <!-- Green pin dot + stem -->
        <div style="display:flex;flex-direction:column;align-items:center;">
          <div style="width:14px;height:14px;background:#22c55e;border-radius:50%;border:2.5px solid #fff;box-shadow:0 2px 10px rgba(34,197,94,0.55);"></div>
          <div style="width:2px;height:16px;background:#22c55e;"></div>
        </div>

        <!-- Polaroid card -->
        <div style="background:#fff;border-radius:14px;box-shadow:0 12px 40px rgba(0,0,0,0.13);overflow:hidden;">
          <div :style="{ background: card.bg }" style="width:100%;height:155px;display:flex;align-items:center;justify-content:center;font-size:62px;">
            {{ card.emoji }}
          </div>
          <div style="padding:12px 14px 14px;">
            <p style="font-size:13px;font-weight:700;color:#111;margin:0 0 3px;">{{ card.label }}</p>
            <p style="font-size:11px;color:#9ca3af;margin:0;line-height:1.4;">{{ card.sub }}</p>
          </div>
        </div>
      </div>

    </section>

    <!-- ═══ LOGO TICKER ═══ -->
    <section style="border-top:1px solid #e5e7eb;padding:28px 0;overflow:hidden;background:rgba(255,255,255,0.5);margin-top:20px;">
      <div style="display:flex;animation:ticker 24s linear infinite;width:max-content;">
        <div v-for="(logo, i) in logos" :key="i"
          style="display:flex;align-items:center;gap:8px;margin:0 40px;white-space:nowrap;color:#9ca3af;font-size:15px;font-weight:700;letter-spacing:-0.3px;">
          <span style="width:8px;height:8px;background:#d1d5db;border-radius:50%;display:inline-block;"></span>
          {{ logo }}
        </div>
      </div>
    </section>

  </div>
</template>

<style scoped>
@keyframes ticker {
  0%   { transform: translateX(0); }
  100% { transform: translateX(-50%); }
}
a[href="#"]:last-of-type:hover {
  background: #16a34a;
}
</style>
