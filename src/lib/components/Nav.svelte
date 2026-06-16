<!-- src/lib/components/Nav.svelte -->
<script>
  // ── Data ──────────────────────────────────────────────────────────
  // Left column services (Visual & Marketing)
  const leftServices = [
    {
      id: 'social-media',
      name: 'Social Media Management',
      count: '/6 services',
      icon: `<svg width="18" height="18" viewBox="0 0 18 18" fill="none">
        <circle cx="4" cy="4" r="1.5" fill="currentColor" opacity=".6"/>
        <circle cx="9" cy="4" r="1.5" fill="currentColor" opacity=".6"/>
        <circle cx="14" cy="4" r="1.5" fill="currentColor" opacity=".6"/>
        <circle cx="4" cy="9" r="1.5" fill="currentColor" opacity=".6"/>
        <circle cx="9" cy="9" r="1.5" fill="currentColor"/>
        <circle cx="14" cy="9" r="1.5" fill="currentColor" opacity=".6"/>
        <circle cx="4" cy="14" r="1.5" fill="currentColor" opacity=".6"/>
        <circle cx="9" cy="14" r="1.5" fill="currentColor" opacity=".6"/>
        <circle cx="14" cy="14" r="1.5" fill="currentColor" opacity=".6"/>
      </svg>`,
      gradient: 'linear-gradient(135deg, #0D1B3E 0%, #1a3a6e 60%, #00B4D8 100%)',
    },
    {
      id: 'branding',
      name: 'Branding & Identity',
      count: '/5 services',
      icon: `<svg width="18" height="18" viewBox="0 0 18 18" fill="none">
        <rect x="1" y="1" width="7" height="7" rx="1" fill="currentColor" opacity=".5"/>
        <rect x="10" y="1" width="7" height="7" rx="1" fill="currentColor" opacity=".8"/>
        <rect x="1" y="10" width="7" height="7" rx="1" fill="currentColor" opacity=".8"/>
        <rect x="10" y="10" width="7" height="7" rx="1" fill="currentColor" opacity=".5"/>
      </svg>`,
      gradient: 'linear-gradient(135deg, #1a0D3E 0%, #3a1a6e 50%, #F4A300 100%)',
    },
    {
      id: 'performance',
      name: 'Performance Marketing',
      count: '/7 services',
      icon: `<svg width="18" height="18" viewBox="0 0 18 18" fill="none">
        <path d="M2 14 L6 8 L10 11 L14 4 L16 6" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" opacity=".7"/>
        <circle cx="14" cy="4" r="2" fill="currentColor" opacity=".8"/>
      </svg>`,
      gradient: 'linear-gradient(135deg, #0D1B3E 0%, #00B4D8 100%)',
    },
    {
      id: 'video',
      name: 'Video Production',
      count: '/4 services',
      icon: `<svg width="18" height="18" viewBox="0 0 18 18" fill="none">
        <rect x="1" y="4" width="11" height="10" rx="2" fill="currentColor" opacity=".6"/>
        <path d="M12 7.5 L17 5 L17 13 L12 10.5 Z" fill="currentColor" opacity=".8"/>
      </svg>`,
      gradient: 'linear-gradient(135deg, #2D1B3E 0%, #6e1a3a 50%, #F4A300 100%)',
    },
  ]

  // Right column services (Digital & Tech)
  const rightServices = [
    {
      id: 'seo',
      name: 'SEO & Content Marketing',
      count: '/6 services',
      icon: `<svg width="18" height="18" viewBox="0 0 18 18" fill="none">
        <circle cx="8" cy="8" r="6" stroke="currentColor" stroke-width="1.5" opacity=".7"/>
        <path d="M13 13 L17 17" stroke="currentColor" stroke-width="2" stroke-linecap="round" opacity=".8"/>
      </svg>`,
    },
    {
      id: 'web',
      name: 'Web Design & Development',
      count: '/7 services',
      icon: `<svg width="18" height="18" viewBox="0 0 18 18" fill="none">
        <rect x="1" y="3" width="16" height="12" rx="2" stroke="currentColor" stroke-width="1.5" opacity=".7"/>
        <path d="M1 7 L17 7" stroke="currentColor" stroke-width="1" opacity=".4"/>
        <circle cx="4" cy="5" r="1" fill="currentColor" opacity=".5"/>
        <circle cx="7" cy="5" r="1" fill="currentColor" opacity=".5"/>
      </svg>`,
    },
    {
      id: 'ai',
      name: 'AI Chatbot & Automation',
      count: '/5 services',
      icon: `<svg width="18" height="18" viewBox="0 0 18 18" fill="none">
        <rect x="3" y="5" width="12" height="9" rx="2" stroke="currentColor" stroke-width="1.5" opacity=".7"/>
        <path d="M6 2 L6 5 M12 2 L12 5" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" opacity=".5"/>
        <circle cx="6.5" cy="9.5" r="1" fill="currentColor" opacity=".7"/>
        <circle cx="11.5" cy="9.5" r="1" fill="currentColor" opacity=".7"/>
      </svg>`,
    },
    {
      id: 'influencer',
      name: 'Influencer Marketing',
      count: '/4 services',
      icon: `<svg width="18" height="18" viewBox="0 0 18 18" fill="none">
        <path d="M9 2 L11 7 L17 7 L12.5 10.5 L14.5 16 L9 12.5 L3.5 16 L5.5 10.5 L1 7 L7 7 Z" stroke="currentColor" stroke-width="1.2" opacity=".7" fill="none"/>
      </svg>`,
    },
  ]

  // ── State ─────────────────────────────────────────────────────────
  let megaOpen = false
  let activeId = 'social-media'   // which service card is expanded
  let closeTimer                  // delay so menu doesn't snap shut

  // ── Handlers ──────────────────────────────────────────────────────
  function openMenu() {
    clearTimeout(closeTimer)
    megaOpen = true
  }

  function scheduleClose() {
    closeTimer = setTimeout(() => { megaOpen = false }, 180)
  }

  function keepOpen() {
    clearTimeout(closeTimer)
  }
</script>

<!-- ════════════════════════════════════════════════════════════════
     ROOT NAV WRAPPER
     position:relative so the mega menu drops from here
════════════════════════════════════════════════════════════════ -->
<nav class="relative z-50 font-sans">

  <!-- ── Top bar ───────────────────────────────────────────────── -->
  <div class="flex items-center bg-[#1c1c1e] border border-white/[0.08] rounded-2xl px-2 py-1.5">

    {#each ['Services', 'Portfolio', 'About', 'Insights', 'Contact'] as item}
      {#if item === 'Services'}
        <!-- Services tab — triggers mega menu on hover -->
        <button
          on:mouseenter={openMenu}
          on:mouseleave={scheduleClose}
          class="relative px-6 py-2 text-[14px] font-medium tracking-wide
                 transition-colors duration-200 rounded-xl
                 {megaOpen
                   ? 'text-white bg-white/10'
                   : 'text-white/70 hover:text-white hover:bg-white/[0.06]'}"
        >
          Services
        </button>
      {:else}
        <a
          href="/{item.toLowerCase()}"
          class="px-6 py-2 text-[14px] font-medium tracking-wide text-white/60
                 hover:text-white transition-colors duration-200 rounded-xl
                 hover:bg-white/[0.05]"
        >
          {item}
        </a>
      {/if}
    {/each}

  </div>

  <!-- ── Mega menu dropdown ────────────────────────────────────── -->
  {#if megaOpen}
    <div
      on:mouseenter={keepOpen}
      on:mouseleave={scheduleClose}
      class="absolute top-[calc(100%+8px)] left-0 right-0
             bg-[#1c1c1e] border border-white/[0.08] rounded-2xl
             overflow-hidden p-3
             grid grid-cols-2 gap-3
             animate-drop"
      role="menu"
    >

      <!-- LEFT COLUMN ─────────────────────────────────────── -->
      <div class="flex flex-col gap-2">
        {#each leftServices as svc}
          <!-- svelte-ignore a11y-no-static-element-interactions -->
          <a
            href="/services/{svc.id}"
            role="menuitem"
            on:mouseenter={() => activeId = svc.id}
            class="group relative rounded-xl overflow-hidden
                   bg-white/[0.04] hover:bg-white/[0.08]
                   border border-white/[0.06] hover:border-white/[0.12]
                   transition-all duration-300 cursor-pointer block"
          >
            <!-- Image panel — expands on hover -->
            <div
              class="overflow-hidden transition-all duration-500 ease-in-out"
              style="max-height: {activeId === svc.id ? '220px' : '0px'};
                     opacity: {activeId === svc.id ? '1' : '0'}"
            >
              <!-- Gradient placeholder — swap for <img> when you have real photos -->
              <div
                class="w-full h-[220px] relative"
                style="background: {svc.gradient}"
              >
                <!-- Decorative circle shapes like the reference -->
                <div class="absolute inset-0 flex items-center justify-center overflow-hidden">
                  <div class="w-[200px] h-[200px] rounded-full border border-white/10
                              flex items-center justify-center">
                    <div class="w-[140px] h-[140px] rounded-full border border-white/[0.08]
                                flex items-center justify-center">
                      <div class="w-[80px] h-[80px] rounded-full bg-white/[0.05]
                                  border border-white/[0.06]"></div>
                    </div>
                  </div>
                </div>
                <!-- Service count badge — top right of image -->
                <span class="absolute top-3 right-3 text-[11px] text-white/40
                             tracking-wider">
                  {svc.count}
                </span>
              </div>
            </div>

            <!-- Label row — always visible -->
            <div class="flex items-center justify-between px-4 py-3.5">
              <div class="flex items-center gap-3">
                <!-- Pixel icon -->
                <span class="text-white/50 group-hover:text-white/80
                             transition-colors flex-shrink-0">
                  {@html svc.icon}
                </span>
                <span class="text-[14px] font-medium text-white/80
                             group-hover:text-white transition-colors
                             tracking-[-0.2px]">
                  {svc.name}
                </span>
              </div>
              <!-- Count shown only when NOT expanded -->
              {#if activeId !== svc.id}
                <span class="text-[11px] text-white/30 tracking-wider flex-shrink-0">
                  {svc.count}
                </span>
              {/if}
            </div>

          </a>
        {/each}
      </div>

      <!-- RIGHT COLUMN ────────────────────────────────────── -->
      <div class="flex flex-col gap-2">
        {#each rightServices as svc}
          <!-- svelte-ignore a11y-no-static-element-interactions -->
          <a
            href="/services/{svc.id}"
            role="menuitem"
            on:mouseenter={() => activeId = svc.id}
            class="group flex items-center justify-between
                   px-4 py-3.5 rounded-xl
                   bg-white/[0.04] hover:bg-white/[0.08]
                   border border-white/[0.06] hover:border-white/[0.12]
                   transition-all duration-200 cursor-pointer
                   flex-1"
            style="min-height: 72px"
          >
            <div class="flex items-center gap-3">
              <span class="text-white/50 group-hover:text-white/80
                           transition-colors flex-shrink-0">
                {@html svc.icon}
              </span>
              <span class="text-[14px] font-medium text-white/80
                           group-hover:text-white transition-colors
                           tracking-[-0.2px]">
                {svc.name}
              </span>
            </div>
            <span class="text-[11px] text-white/30 tracking-wider flex-shrink-0 ml-3">
              {svc.count}
            </span>
          </a>
        {/each}
      </div>

    </div>
  {/if}

</nav>

<style>
  /* Drop animation — menu slides down from top */
  @keyframes drop {
    from {
      opacity: 0;
      transform: translateY(-8px);
    }
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }

  .animate-drop {
    animation: drop 0.2s ease forwards;
  }
</style>