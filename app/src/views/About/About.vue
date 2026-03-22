<script lang="ts">
    import "./about.css";

    export default {
    name: "About",
    setup() {
        const architectureItems = [
        { label: "Framework", value: "React" },
        { label: "Build Tool", value: "Vite" },
        { label: "Security", value: "OAuth 2.0" },
        ];

        return { architectureItems };
    },
    };
</script>

<template>
  <div>
    <div class="home-page-container">
      <div class="home-content-wrapper">
        <section class="home-section-hero">
          <span>The Sonic Curator</span>
          <h1>
            Your Music.<br />
            Visualized.
          </h1>
          <p>
            Transforming your Spotify listening history into high-end editorial gallery pieces.
          </p>
        </section>

        <div>
          <div />
          <img
            src="https://picsum.photos/seed/about/1200/600"
            alt="Abstract visualization"
            referrerpolicy="no-referrer"
          />
        </div>

        <section>
          <div>
            <h2>The Vision</h2>
            <p>
              Spotify Collage was born from the idea that music isn't just audio—it's an aesthetic journey. We leverage the
              <span>Spotify Web API</span> to pull your top tracks, artists, and recently played albums, converting that metadata into stunning, high-resolution wallpaper collages.
            </p>
          </div>

          <div>
            <h2>Architecture</h2>
            <div>
              <div v-for="item in architectureItems" :key="item.label">
                <span>{{ item.label }}</span>
                <span>{{ item.value }}</span>
              </div>
            </div>
            <p>
              Built for speed and performance, ensuring your art is generated in real-time without the bloat.
            </p>
          </div>

          <div>
            <p>
              "We believe your data should be as beautiful as the music that created it. This isn't just a list; it's your sonic history, curated."
            </p>
          </div>
        </section>

        <section>
          <div />
          <h3>Ready to see your sound?</h3>
          <router-link to="/create">
            Create Your First Collage
          </router-link>
        </section>
      </div>
    </div>
  </div>
</template>
