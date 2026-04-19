<template>
  <nav>
    <!-- Header -->
    <div class="flex items-center justify-between gap-4 max-w-7xl mx-auto py-4 px-6">
      <div>
        <img src="/logo.jpg" height="170px" width="170px" />
      </div>

      <div>
        <a href="tel:+0886616931"
          class="px-5 py-3 rounded-lg bg-violet-600 text-white text-sm font-medium hover:opacity-90 transition">
          Contact Sales
        </a>
      </div>

    </div>
  </nav>
  <div class="max-w-7xl mx-auto">
    <slot />
  </div>


  <!-- Apple-style Footer -->
  <footer class="footer">
    <div class="footer-inner">

      <!-- Top: Brand + Nav columns -->
      <div class="footer-top">
        <div class="footer-brand">
          <div class="brand-mark">OTG</div>
          <p class="brand-tagline">Ignite your future.</p>
        </div>

        <div class="footer-nav">
          <div class="nav-col">
            <span class="nav-heading">Company</span>
            <a href="#">About</a>
            <a href="#">Products</a>
            <a href="#">Installations</a>
          </div>
          <div class="nav-col">
            <span class="nav-heading">Support</span>
            <a href="#">Contact</a>
            <a href="#">Help Center</a>
            <a href="#">Service Request</a>
          </div>
          <div class="nav-col">
            <span class="nav-heading">Locations</span>
            <a href="#">Blantyre</a>
            <a href="#">Lilongwe</a>
            <a href="#">Mzuzu</a>
            <a href="#">Karonga</a>
          </div>
        </div>
      </div>

      <!-- Divider -->
      <div class="footer-divider"></div>

      <!-- Bottom bar -->
      <div class="footer-bottom">
        <p class="footer-copy">© {{ new Date().getFullYear() }} OTG 4 U. All rights reserved.</p>

        <div class="footer-meta">
          <a href="#">Privacy Policy</a>
          <span class="sep">|</span>
          <a href="#">Terms of Use</a>
          <span class="sep">|</span>
          <span>+265 995 441 381</span>
        </div>
      </div>

    </div>
  </footer>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=SF+Pro+Display:wght@300;400;500&display=swap');

/* ── Root tokens ── */
.footer {
  --fg: #1d1d1f;
  --fg-muted: #6e6e73;
  --fg-dim: #aeaeb2;
  --border: #d2d2d7;
  --accent: #7c3aed;
  --bg: #f5f5f7;

  background: var(--bg);
  border-top: 1px solid var(--border);
  font-family: -apple-system, 'Helvetica Neue', sans-serif;
  -webkit-font-smoothing: antialiased;
}

/* Dark mode */
@media (prefers-color-scheme: dark) {
  .footer {
    --fg: #f5f5f7;
    --fg-muted: #a1a1a6;
    --fg-dim: #6e6e73;
    --border: #3a3a3c;
    --bg: #161617;
  }
}

.footer-inner {
  max-width: 980px;
  margin: 0 auto;
  padding: 48px 24px 28px;
}

/* ── Top section ── */
.footer-top {
  display: flex;
  gap: 64px;
  align-items: flex-start;
}

/* Brand */
.footer-brand {
  flex-shrink: 0;
  min-width: 160px;
}

.brand-mark {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 40px;
  height: 40px;
  border-radius: 10px;
  background: var(--accent);
  color: #fff;
  font-size: 11px;
  font-weight: 600;
  letter-spacing: 0.05em;
  margin-bottom: 12px;
}

.brand-tagline {
  font-size: 13px;
  color: var(--fg-muted);
  margin: 0;
  font-weight: 400;
  line-height: 1.4;
  max-width: 140px;
}

/* Nav columns */
.footer-nav {
  display: flex;
  gap: 48px;
  flex-wrap: wrap;
  flex: 1;
}

.nav-col {
  display: flex;
  flex-direction: column;
  gap: 10px;
  min-width: 120px;
}

.nav-heading {
  font-size: 12px;
  font-weight: 600;
  color: var(--fg);
  letter-spacing: 0.01em;
  margin-bottom: 2px;
}

.nav-col a {
  font-size: 12px;
  color: var(--fg-muted);
  text-decoration: none;
  transition: color 0.15s ease;
  line-height: 1.5;
}

.nav-col a:hover {
  color: var(--accent);
}

/* ── Divider ── */
.footer-divider {
  height: 1px;
  background: var(--border);
  margin: 36px 0 20px;
}

/* ── Bottom bar ── */
.footer-bottom {
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: wrap;
  gap: 12px;
}

.footer-copy {
  font-size: 12px;
  color: var(--fg-dim);
  margin: 0;
}

.footer-meta {
  display: flex;
  align-items: center;
  gap: 8px;
  font-size: 12px;
  color: var(--fg-dim);
  flex-wrap: wrap;
}

.footer-meta a {
  color: var(--fg-dim);
  text-decoration: none;
  transition: color 0.15s ease;
}

.footer-meta a:hover {
  color: var(--accent);
}

.sep {
  color: var(--border);
}

/* ── Responsive ── */
@media (max-width: 640px) {
  .footer-top {
    flex-direction: column;
    gap: 32px;
  }

  .footer-nav {
    gap: 32px;
  }

  .footer-bottom {
    flex-direction: column;
    align-items: flex-start;
    gap: 8px;
  }
}
</style>