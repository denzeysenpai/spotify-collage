<script setup lang="ts">
import { RouterLink, RouterView, useRoute } from 'vue-router'

const route = useRoute()

const navLinks = [
  { name: 'Home', path: '/' },
  { name: 'Create', path: '/create' },
  { name: 'About', path: '/about' },
]

const isActiveLink = (path: string) => {
  return route.path === path
}
</script>

<template>
  <header class="navbar">
    <nav class="navbar-content">
      <RouterLink to="/" class="navbar-brand">
        Spotify Collage
      </RouterLink>
      
      <div class="navbar-links">
        <RouterLink
          v-for="link in navLinks"
          :key="link.path"
          :to="link.path"
          :class="['navbar-link', { 'navbar-link--active': isActiveLink(link.path) }]"
        >
          {{ link.name }}
        </RouterLink>
      </div>

      <div class="navbar-actions">
        <button class="navbar-user-btn">
          <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"></path>
            <circle cx="12" cy="7" r="4"></circle>
          </svg>
        </button>
        <RouterLink to="/create" class="navbar-cta">
          Get Started
        </RouterLink>
      </div>
    </nav>
  </header>

  <main class="main-content">
    <RouterView />
  </main>

  <footer class="footer">
    <div class="footer-content">
      <div class="footer-links">
        <RouterLink to="/privacy" class="footer-link">Privacy</RouterLink>
        <a href="https://github.com" class="footer-link" target="_blank" rel="noopener noreferrer">Github</a>
        <RouterLink to="/terms" class="footer-link">Terms</RouterLink>
      </div>
      <div class="footer-brand">Spotify Collage</div>
      <p class="footer-copyright">
        © 2026 Spotify Collage. Editorial curation for your sonic history. Built for the modern collector.
      </p>
    </div>
  </footer>
</template>

<style scoped>
.navbar {
  position: fixed;
  top: 0;
  width: 100%;
  z-index: 50;
  background: rgba(25, 20, 20, 0.6);
  backdrop-filter: blur(16px);
  box-shadow: 0px 0px 40px rgba(255, 255, 255, 0.08);
}

.navbar-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 2rem;
  width: 100%;
  max-width: 1280px;
  margin: 0 auto;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  font-weight: 500;
  letter-spacing: -0.025em;
}

.navbar-brand {
  font-size: 1.5rem;
  font-weight: 700;
  letter-spacing: -0.05em;
  color: #1ed760;
  text-decoration: none;
  transition: var(--delay-sm);
}

.navbar-links {
  display: flex;
  align-items: center;
  gap: 2rem;
}

.navbar-link {
  color: rgba(255, 255, 255, 0.7);
  text-decoration: none;
  font-weight: 500;
  padding: 0.25rem 0;
  transition: var(--delay-sm);
  position: relative;
}

.navbar-link--active {
  color: #1ed760;
  border-bottom: 2px solid #1ed760;
  padding-bottom: 0.25rem;
}

.navbar-link:hover:not(.navbar-link--active) {
  color: #ffffff;
}

.navbar-actions {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.navbar-user-btn {
  background: none;
  border: none;
  color: rgba(255, 255, 255, 0.7);
  cursor: pointer;
  padding: 0.5rem;
  border-radius: 0.5rem;
  transition: var(--delay-sm);
  display: flex;
  align-items: center;
  justify-content: center;
}

.navbar-user-btn:hover {
  color: #ffffff;
  background: rgba(255, 255, 255, 0.1);
}

.navbar-user-btn:active {
  transform: scale(0.95);
}

.navbar-cta {
  background: linear-gradient(to bottom right, #1db954, #1ed760);
  color: #ffffff;
  text-decoration: none;
  padding: 0.5rem 1.5rem;
  border-radius: 9999px;
  font-weight: 700;
  font-size: 0.875rem;
  transition: transform 0.2s ease;
  display: inline-block;
}

.navbar-cta:active {
  transform: scale(0.95);
}

.main-content {
  padding-top: 80px;
}

/* Footer Styles */
.footer {
  width: 100%;
  padding: 3rem 0;
  background: rgba(255, 255, 255, 0.05);
  margin-top: 6rem;
}

.footer-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 1.5rem;
  width: 100%;
  max-width: 1280px;
  margin: 0 auto;
  padding: 0 2rem;
}

.footer-links {
  display: flex;
  gap: 3rem;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  font-size: 0.6875rem;
  text-transform: uppercase;
  letter-spacing: 0.05em;
}

.footer-link {
  color: rgba(255, 255, 255, 0.7);
  text-decoration: none;
  transition: opacity 0.2s ease;
}

.footer-link:hover {
  color: #1ed760;
  opacity: 0.8;
}

.footer-brand {
  color: #1ed760;
  font-weight: 700;
  letter-spacing: -0.05em;
  font-size: 1.25rem;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
}

.footer-copyright {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  font-size: 0.6875rem;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  color: rgba(255, 255, 255, 0.7);
  text-align: center;
  max-width: 28rem;
  line-height: 1.4;
}

@media (max-width: 768px) {
  .navbar-content {
    padding: 1rem;
  }
  
  .navbar-links {
    display: none;
  }
  
  .navbar-brand {
    font-size: 1.25rem;
  }
  
  .navbar-cta {
    padding: 0.5rem 1rem;
    font-size: 0.75rem;
  }
  
  .main-content {
    padding-top: 70px;
  }
  
  .footer-content {
    padding: 0 1rem;
    gap: 1rem;
  }
  
  .footer-links {
    gap: 1.5rem;
  }
  
  .footer-brand {
    font-size: 1.125rem;
  }
  
  .footer-copyright {
    font-size: 0.625rem;
  }
}
</style>

