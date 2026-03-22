<script setup lang="ts">
    import "./create.css";
    import { ref, computed, onMounted } from 'vue';

    const albums = [
      { id: 1, title: 'After Hours', artist: 'The Weeknd', src: 'https://picsum.photos/seed/afterhours/800/800', size: 'large' },
      { id: 2, title: 'Future Nostalgia', artist: 'Dua Lipa', src: 'https://picsum.photos/seed/future/600/600', size: 'small' },
      { id: 3, title: 'Fine Line', artist: 'Harry Styles', src: 'https://picsum.photos/seed/fineline/600/600', size: 'small' },
      { id: 4, title: 'Plastic Hearts', artist: 'Miley Cyrus', src: 'https://picsum.photos/seed/plastic/800/400', size: 'wide' },
      { id: 5, title: 'Folklore', artist: 'Taylor Swift', src: 'https://picsum.photos/seed/folklore/600/600', size: 'small' },
      { id: 6, title: 'Positions', artist: 'Ariana Grande', src: 'https://picsum.photos/seed/positions/600/600', size: 'small' },
      { id: 7, title: 'After Hours', artist: 'The Weeknd', src: 'https://picsum.photos/seed/afterhours/800/800', size: 'large' },
      { id: 8, title: 'Future Nostalgia', artist: 'Dua Lipa', src: 'https://picsum.photos/seed/future/600/600', size: 'small' },
      { id: 9, title: 'Fine Line', artist: 'Harry Styles', src: 'https://picsum.photos/seed/fineline/600/600', size: 'small' },
      { id: 10, title: 'Plastic Hearts', artist: 'Miley Cyrus', src: 'https://picsum.photos/seed/plastic/800/400', size: 'wide' },
    
    ];

    const layout = ref('grid');
    const grayscale = ref(false);
    const colorOverlay = ref(true);
    const spacing = ref(32);
    const aspectRatio = ref('1:1');
    const borderRadius = ref(12);

    const gridClasses = computed(() => {
      switch (layout.value) {
        case 'grid':
          return 'grid-cols-auto-fit';
        case 'mosaic':
          return 'grid-cols-auto-fit-mosaic';
        case 'chaotic':
          return 'grid-cols-auto-fit-chaotic';
        default:
          return 'grid-cols-auto-fit';
      }
    });

    const albumClasses = (album: any) => {
      let classes = 'album-item';
      if (album.size === 'large') {
        classes += ' album-item--large';
      } else if (album.size === 'wide') {
        classes += ' album-item--wide';
      }
      if (spacing.value === 0) {
        classes += ' album-item--no-radius';
      }
      return classes;
    };

    const aspectRatioStyle = computed(() => {
      switch (aspectRatio.value) {
        case '4:5':
          return { aspectRatio: '4/5' };
        case '16:9':
          return { aspectRatio: '16/9' };
        case '1:1':
        default:
          return { aspectRatio: '1/1' };
      }
    });

    const setLayout = (newLayout: string) => {
      layout.value = newLayout;
    };

    const toggleGrayscale = () => {
      grayscale.value = !grayscale.value;
      colorOverlay.value = !grayscale.value;
    };

    const toggleColorOverlay = () => {
      colorOverlay.value = !colorOverlay.value;
      grayscale.value = !colorOverlay.value;
    };

    const setAspectRatio = (ratio: string) => {
      aspectRatio.value = ratio;
    };

    const updateSpacing = (event: Event) => {
      const target = event.target as HTMLInputElement;
      spacing.value = parseInt(target.value);
    };

    const updateBorderRadius = (event: Event) => {
      const target = event.target as HTMLInputElement;
      borderRadius.value = parseInt(target.value);
    };

    const sidebarOpen = ref(false);

    const toggleSidebar = () => {
      sidebarOpen.value = !sidebarOpen.value;
    };

    onMounted(() => {
      // Add entrance animations
      document.body.classList.add('loaded');
    });
</script>

<template>
  <div class="create-view">
    
    <!-- Main Canvas -->
    <main class="main-canvas">
      <div class="canvas-container">
        <div class="canvas-header">
          <div>
            <span class="canvas-label">Live Preview</span>
            <h1 class="canvas-title">The Sonic Archive</h1>
          </div>
          <div class="stats">
            <div class="stat">
              <p class="stat-label">Total Plays</p>
              <p class="stat-value">12,482</p>
            </div>
            <div class="stat">
              <p class="stat-label">Artists</p>
              <p class="stat-value">148</p>
            </div>
          </div>
        </div>

        <!-- Grid Container -->
        <div 
          :class="['album-grid', gridClasses]"
          :style="{ gap: `${spacing}px` }"
        >
          <div
            v-for="album in albums"
            :key="album.id"
            :class="albumClasses(album)"
            :style="{ 
              borderRadius: spacing === 0 ? '0' : `${borderRadius}px`,
              ...aspectRatioStyle 
            }"
          >
            <img 
              :src="album.src" 
              :alt="album.title" 
              :class="['album-image', { 'album-image--grayscale': grayscale }]"
              referrerpolicy="no-referrer"
            />
            <div class="album-overlay">
              <p class="album-title">{{ album.title }}</p>
              <p class="album-artist">{{ album.artist }}</p>
            </div>
          </div>
        </div>

        <!-- Controls Overlay -->
        <div class="controls-overlay">
          <div class="controls-left">
            <div class="control-group">
              <span class="control-label">Layout</span>
              <div class="layout-buttons">
                <button
                  @click="setLayout('grid')"
                  :class="['layout-btn', { 'layout-btn--active': layout === 'grid' }]"
                >
                  <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <rect x="3" y="3" width="7" height="7"/>
                    <rect x="14" y="3" width="7" height="7"/>
                    <rect x="14" y="14" width="7" height="7"/>
                    <rect x="3" y="14" width="7" height="7"/>
                  </svg>
                  Grid
                </button>
                <button
                  @click="setLayout('mosaic')"
                  :class="['layout-btn', { 'layout-btn--active': layout === 'mosaic' }]"
                >
                  <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <rect x="3" y="3" width="18" height="7"/>
                    <rect x="3" y="14" width="8" height="7"/>
                    <rect x="14" y="14" width="7" height="7"/>
                  </svg>
                  Mosaic
                </button>
                <button
                  @click="setLayout('chaotic')"
                  :class="['layout-btn', { 'layout-btn--active': layout === 'chaotic' }]"
                >
                  <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <rect x="3" y="3" width="5" height="5"/>
                    <rect x="10" y="3" width="5" height="5"/>
                    <rect x="17" y="3" width="4" height="5"/>
                    <rect x="3" y="10" width="7" height="5"/>
                    <rect x="12" y="10" width="5" height="5"/>
                    <rect x="3" y="17" width="5" height="4"/>
                    <rect x="10" y="17" width="5" height="4"/>
                    <rect x="17" y="17" width="4" height="4"/>
                  </svg>
                  Chaotic
                </button>
              </div>
            </div>
            <div class="control-divider" />
            <div class="control-group">
              <span class="control-label">Color</span>
              <div class="color-buttons">
                                <button :class="['color-btn', { 'color-btn--active': !grayscale }]" @click="toggleGrayscale">
                  <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <path d="M12 2.69l5.66 5.66a8 8 0 1 1-11.31 0z"/>
                  </svg>
                  Color
                </button>
                <button
                  @click="toggleGrayscale"
                  :class="['color-btn', { 'color-btn--active': grayscale }]"
                >
                  <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <line x1="4" y1="21" x2="4" y2="14"/>
                    <line x1="4" y1="10" x2="4" y2="3"/>
                    <line x1="12" y1="21" x2="12" y2="12"/>
                    <line x1="12" y1="8" x2="12" y2="3"/>
                    <line x1="20" y1="21" x2="20" y2="16"/>
                    <line x1="20" y1="12" x2="20" y2="3"/>
                    <line x1="1" y1="14" x2="7" y2="14"/>
                    <line x1="9" y1="8" x2="15" y2="8"/>
                    <line x1="17" y1="16" x2="23" y2="16"/>
                  </svg>
                  Grayscale
                </button>

              </div>
            </div>
            <div class="control-divider" />
            <div class="control-group">
              <span class="control-label">Aspect Ratio</span>
              <div class="aspect-ratio-buttons">
                <button
                  v-for="ratio in ['1:1', '4:5', '16:9']"
                  :key="ratio"
                  @click="setAspectRatio(ratio)"
                  :class="['ratio-btn', { 'ratio-btn--active': aspectRatio === ratio }]"
                >
                  {{ ratio }}
                </button>
              </div>
            </div>
            <div class="control-divider" />
            <div class="control-group">
              <span class="control-label">Grid Spacing</span>
              <input 
                type="range" 
                min="0" 
                max="64" 
                :value="spacing"
                @input="updateSpacing"
                class="spacing-slider"
              />
            </div>
            <div class="control-divider" />
            <div class="control-group">
              <span class="control-label">Border Radius</span>
              <input 
                type="range" 
                min="0" 
                max="24" 
                :value="borderRadius"
                @input="updateBorderRadius"
                class="border-radius-slider"
              />
            </div>
          </div>
          <div class="controls-right">
            <button class="regenerate-btn">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <path d="M23 4v6h-6M1 20v-6h6"/>
                <path d="M3.51 9a9 9 0 0 1 14.85-3.36L23 10M1 14l4.64 4.36A9 9 0 0 0 20.49 15"/>
              </svg>
              <span>Regenerate</span>
            </button>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>