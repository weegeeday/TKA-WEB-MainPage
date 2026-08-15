<script setup lang="ts">
import { ref } from 'vue'

const gameUrl = 'https://game.technokittenadventure.ca'
const repo1Url = 'https://github.com/shadowartist201/TKA-PC-Port'
const repo2Url = 'https://github.com/weegeeday/TKA-PC-Port-Web'
const donateUrl = 'https://buymeacoffee.com/shadowartist201'
const topImage = '/top-image.png'

const showControlsModal = ref(false)

function isMobileDevice(): boolean {
  if (typeof window === 'undefined') return false
  const userAgent = navigator.userAgent || navigator.vendor || (window as any).opera || ''
  const isTouchScreen = 'ontouchstart' in window || navigator.maxTouchPoints > 0
  const isMobileUA = /Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(userAgent)
  return isMobileUA || (isTouchScreen && window.innerWidth <= 768)
}

function handlePlayClick(event: MouseEvent) {
  event.preventDefault()
  if (isMobileDevice()) {
    window.location.href = gameUrl
  } else {
    showControlsModal.value = true
  }
}

function proceedToGame() {
  window.location.href = gameUrl
}

function closeModal() {
  showControlsModal.value = false
}
</script>

<template>
  <div class="layout">
    <!-- Top Left Title -->
    <header class="header">
      <h1 class="site-title">Techno Kitten Adventure</h1>
    </header>

    <main class="content">
      <!-- Top Section: Centered Image and Play Button -->
      <section class="section top-section">
        <div class="image-container">
          <img 
            :src="topImage" 
            alt="Techno Kitten Adventure" 
            class="centered-image"
          />
        </div>
        <div class="action-container">
          <a 
            :href="gameUrl" 
            class="btn btn-primary"
            @click="handlePlayClick"
          >
            Play Game &rarr;
          </a>
        </div>
      </section>

      <!-- Bottom Section: GitHub Repositories (List view, No Cards) -->
      <section class="section bottom-section">
        <h2 class="section-heading">GitHub Repositories</h2>

        <div class="repo-list">
          <!-- Repo Item 1 -->
          <div class="repo-item">
            <div class="repo-meta">
              <h3 class="repo-title">
                <a :href="repo1Url" target="_blank" rel="noopener noreferrer">
                  shadowartist201 / TKA-PC-Port
                </a>
              </h3>
              <p class="repo-description">
                PC port of Techno Kitten Adventure, web version is based on this.
              </p>
            </div>
            <div class="repo-actions">
              <a 
                :href="donateUrl" 
                target="_blank" 
                rel="noopener noreferrer" 
                class="btn btn-donate"
              >
                Donate
              </a>
            </div>
          </div>

          <!-- Repo Item 2 -->
          <div class="repo-item">
            <div class="repo-meta">
              <h3 class="repo-title">
                <a :href="repo2Url" target="_blank" rel="noopener noreferrer">
                  weegeeday / TKA-PC-Port-Web
                </a>
              </h3>
              <p class="repo-description">
                Web port of Techno Kitten Adventure.
              </p>
            </div>
          </div>
        </div>
      </section>
    </main>

    <!-- Controls Popup Modal (PC only) -->
    <Teleport to="body">
      <div 
        v-if="showControlsModal" 
        class="modal-backdrop" 
        @click.self="closeModal"
      >
        <div class="modal-content" role="dialog" aria-modal="true">
          <div class="modal-header">
            <h2 class="modal-title">Game Controls</h2>
            <button class="close-btn" @click="closeModal" aria-label="Close">&times;</button>
          </div>

          <div class="modal-body">
            <div class="control-row">
              <span class="control-label">Mouse / Touch</span>
              <span class="control-value">Click buttons / use mouse</span>
            </div>

            <div class="control-row">
              <span class="control-label">Start</span>
              <span class="control-value"><kbd>S</kbd></span>
            </div>

            <div class="control-row">
              <span class="control-label">A Button</span>
              <span class="control-value"><kbd>Spacebar</kbd></span>
            </div>

            <div class="control-row">
              <span class="control-label">B Button</span>
              <span class="control-value"><kbd>B</kbd></span>
            </div>
          </div>

          <div class="modal-footer">
            <button class="btn btn-secondary" @click="closeModal">Cancel</button>
            <button class="btn btn-primary modal-play-btn" @click="proceedToGame">Play Now &rarr;</button>
          </div>
        </div>
      </div>
    </Teleport>
  </div>
</template>

<style scoped>
.layout {
  width: 100%;
  max-width: 800px;
  margin: 0 auto;
  padding: 1.5rem 1.25rem 3rem 1.25rem;
}

.header {
  margin-bottom: 2rem;
  text-align: left;
}

.site-title {
  font-size: 1.5rem;
  font-weight: 700;
  letter-spacing: -0.01em;
  color: var(--text-main);
}

.section {
  margin-bottom: 3rem;
}

.top-section {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1.5rem;
  width: 100%;
}

.image-container {
  width: 100%;
  max-width: 640px;
  display: flex;
  justify-content: center;
}

.centered-image {
  max-width: 100%;
  height: auto;
  display: block;
}

.action-container {
  display: flex;
  justify-content: center;
}

.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 0.75rem 1.75rem;
  font-size: 0.95rem;
  font-weight: 600;
  text-decoration: none;
  transition: all 0.15s ease;
  cursor: pointer;
  border-radius: 0;
}

.btn-primary {
  background-color: var(--text-main);
  color: var(--bg-color);
  border: 1px solid var(--text-main);
}

.btn-primary:hover {
  background-color: #ffffff;
  opacity: 0.9;
}

.btn-donate {
  background-color: transparent;
  color: var(--text-main);
  border: 1px solid var(--border-color);
  padding: 0.5rem 1.25rem;
  font-size: 0.875rem;
}

.btn-donate:hover {
  border-color: var(--text-main);
  background-color: var(--bg-secondary);
}

.bottom-section {
  text-align: left;
  border-top: 1px solid var(--border-color);
  padding-top: 2rem;
}

.section-heading {
  font-size: 1.05rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  color: var(--text-muted);
  margin-bottom: 1.25rem;
}

.repo-list {
  display: flex;
  flex-direction: column;
}

.repo-item {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  gap: 1.5rem;
  padding: 1.25rem 0;
  border-bottom: 1px solid var(--border-color);
}

.repo-meta {
  display: flex;
  flex-direction: column;
  gap: 0.35rem;
  flex: 1;
  min-width: 0;
}

.repo-title {
  font-size: 1.05rem;
  font-weight: 600;
}

.repo-title a {
  color: var(--text-main);
}

.repo-title a:hover {
  text-decoration: underline;
}

.repo-description {
  font-size: 0.9rem;
  color: var(--text-muted);
  max-width: 600px;
}

.repo-actions {
  margin-top: 0.25rem;
  flex-shrink: 0;
}

/* Modal Styles */
.modal-backdrop {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: rgba(0, 0, 0, 0.85);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
  padding: 1rem;
  overflow-y: auto;
}

.modal-content {
  background-color: #181818;
  border: 1px solid var(--border-color);
  width: 100%;
  max-width: 440px;
  padding: 1.75rem;
  color: var(--text-main);
  text-align: left;
}

.modal-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1.25rem;
  padding-bottom: 0.75rem;
  border-bottom: 1px solid var(--border-color);
}

.modal-title {
  font-size: 1.15rem;
  font-weight: 700;
  letter-spacing: -0.01em;
}

.close-btn {
  background: none;
  border: none;
  color: var(--text-muted);
  font-size: 1.5rem;
  line-height: 1;
  cursor: pointer;
  padding: 0;
}

.close-btn:hover {
  color: var(--text-main);
}

.modal-body {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  margin-bottom: 1.75rem;
}

.control-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-bottom: 0.6rem;
  border-bottom: 1px dashed var(--border-color);
  gap: 1rem;
}

.control-label {
  font-size: 0.9rem;
  color: var(--text-muted);
}

.control-value {
  font-size: 0.9rem;
  font-weight: 600;
}

kbd {
  display: inline-block;
  background-color: #262626;
  border: 1px solid #404040;
  padding: 0.2rem 0.5rem;
  font-family: monospace;
  font-size: 0.85rem;
  color: #ffffff;
}

.modal-footer {
  display: flex;
  justify-content: flex-end;
  gap: 0.75rem;
}

.btn-secondary {
  background-color: transparent;
  color: var(--text-muted);
  border: 1px solid var(--border-color);
  padding: 0.6rem 1.25rem;
  font-size: 0.875rem;
}

.btn-secondary:hover {
  color: var(--text-main);
  border-color: var(--text-main);
}

@media (max-width: 640px) {
  .layout {
    padding: 1.25rem 1rem 2.5rem 1rem;
  }

  .header {
    margin-bottom: 1.5rem;
  }

  .site-title {
    font-size: 1.25rem;
  }

  .section {
    margin-bottom: 2rem;
  }

  .repo-item {
    flex-direction: column;
    align-items: flex-start;
    gap: 0.75rem;
  }

  .repo-actions {
    margin-top: 0.25rem;
  }
}
</style>
