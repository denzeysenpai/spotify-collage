<script setup lang="ts">
import "./home.css";
import { ref, onMounted } from 'vue';

const albumImages = [
  'https://picsum.photos/seed/album1/600/600',
  'https://picsum.photos/seed/album2/600/600',
  'https://picsum.photos/seed/album3/600/600',
  'https://picsum.photos/seed/album4/600/600',
  'https://picsum.photos/seed/album5/600/600',
  'https://picsum.photos/seed/album6/600/600',
];

onMounted(() => {
  // Add entrance animations
  document.body.classList.add('loaded');
});
</script>

<template>
  <div class="home-landing">
    <!-- Hero Section -->
    <section class="hero-section">
      <div class="hero-background" />
      
      <div class="hero-content">
        <h1 class="hero-title">
          Curate Your <span class="hero-title-highlight">Sonic Story</span>
        </h1>
        
        <p class="hero-description">
          Transform your listening habits into high-fidelity editorial art. Connect your Spotify account to generate beautiful, custom album art collages of your most played tracks.
        </p>
        
        <div class="hero-actions">
          <button class="btn-primary">
            <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <path d="M23 4v6h-6M1 20v-6h6"/>
              <path d="M3.51 9a9 9 0 0 1 14.85-3.36L23 10M1 14l4.64 4.36A9 9 0 0 0 20.49 15"/>
            </svg>
            Connect with Spotify
          </button>
          <router-link to="/gallery" class="btn-secondary">
            View Gallery
          </router-link>
        </div>
      </div>

      <!-- Album Grid Preview -->
      <div class="album-grid">
        <div 
          v-for="(src, i) in albumImages" 
          :key="i" 
          :class="['album-item', { 'album-item--offset': i % 2 === 1 }]"
        >
          <img :src="src" :alt="`Album ${i}`" referrerpolicy="no-referrer" />
          <div class="album-overlay">
            <p class="album-label">Album {{ i + 1 }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Features Bento Grid -->
    <section class="features-section">
      <div class="features-grid">
        <div class="feature-card feature-card--large">
          <div class="feature-content">
            <div class="feature-badge">Automated Curation</div>
            <h3 class="feature-title">Your entire history, visualized.</h3>
            <p class="feature-description">
              We scan your top artists, albums, and tracks across any timeframe to build a visual representation of your unique sonic identity.
            </p>
          </div>
          <div class="feature-footer">
            <div class="feature-icon">
              <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <polygon points="12 2 15.09 8.26 22 9.27 17 14.14 18.18 21.02 12 17.77 5.82 21.02 7 14.14 2 9.27 8.91 8.26 12 2"/>
              </svg>
            </div>
            <span class="feature-label">Smart Layout Engine</span>
          </div>
        </div>

        <div class="feature-card feature-card--center">
          <svg width="48" height="48" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" class="feature-icon-large">
            <circle cx="12" cy="8" r="7"/>
            <polyline points="8.21 13.89 7 23 12 20 17 23 15.79 13.88"/>
          </svg>
          <h4 class="feature-subtitle">High Fidelity</h4>
          <p class="feature-text">Export your collages in up to 4K resolution, perfect for print or digital wallpaper.</p>
        </div>

        <div class="feature-card">
          <div class="feature-icon-box">
            <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <path d="M12 2L2 7l10 5 10-5-10-5z"/>
              <path d="M2 17l10 5 10-5M2 12l10 5 10-5"/>
            </svg>
          </div>
          <div>
            <h4 class="feature-subtitle">Custom Styles</h4>
            <p class="feature-text">Choose from Grid, Mosaic, or Chaotic layouts to match your aesthetic.</p>
          </div>
        </div>

        <div class="feature-card feature-card--wide">
          <div class="feature-content-inline">
            <div>
              <h3 class="feature-title-inline">Ready for Sharing</h3>
              <p class="feature-description-inline">
                One-click export tailored for Instagram Stories, Twitter headers, and more.
              </p>
              <button class="feature-link">
                Explore layouts 
                <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <line x1="5" y1="12" x2="19" y2="12"/>
                  <polyline points="12 5 19 12 12 19"/>
                </svg>
              </button>
            </div>
          </div>
          <div class="feature-gradient" />
        </div>
      </div>
    </section>

    <!-- CTA Section -->
    <section class="cta-section">
      <div class="cta-card">
        <div class="cta-background" />
        <div class="cta-content">
          <h2 class="cta-title">Ready to see your music?</h2>
          <button class="cta-button">
            Connect with Spotify
          </button>
        </div>
      </div>
    </section>
  </div>
</template>
