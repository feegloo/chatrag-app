<template>
  <div class="home-header-actions">
    <button
      v-if="show"
      class="home-lang-toggle"
      :title="t.switchTitle"
      :aria-label="t.switchTitle"
      @click="toggleHomeLang"
    >
      <span class="home-lang-flag">{{ flag }}</span>
    </button>
    <a
      class="home-github-link"
      href="https://github.com/feegloo/chatrag-app"
      target="_blank"
      rel="noopener noreferrer"
      :title="githubLabel"
      :aria-label="githubLabel"
    >
      <svg
        width="22"
        height="22"
        viewBox="0 0 24 24"
        fill="currentColor"
        aria-hidden="true"
      >
        <path
          d="M12 .297C5.37.297 0 5.67 0 12.297c0 5.303 3.438 9.8 8.205 11.385.6.113.82-.258.82-.577 0-.285-.01-1.04-.015-2.04-3.338.724-4.043-1.61-4.043-1.61-.546-1.387-1.333-1.756-1.333-1.756-1.09-.745.083-.729.083-.729 1.205.084 1.838 1.237 1.838 1.237 1.07 1.835 2.809 1.305 3.495.998.108-.776.418-1.305.762-1.605-2.665-.305-5.467-1.334-5.467-5.931 0-1.31.469-2.381 1.236-3.221-.124-.303-.536-1.524.117-3.176 0 0 1.008-.323 3.301 1.23a11.52 11.52 0 0 1 3.003-.404c1.02.005 2.045.138 3.003.404 2.291-1.553 3.297-1.23 3.297-1.23.655 1.652.243 2.873.12 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222 0 1.606-.015 2.898-.015 3.293 0 .322.216.694.825.576C20.565 22.092 24 17.597 24 12.297c0-6.627-5.373-12-12-12"
        />
      </svg>
    </a>
  </div>
</template>

<script setup lang="ts">
import { computed } from "vue";
import { homeLang, homeT, toggleHomeLang } from "../i18n/homeLocale";

const t = homeT;
const githubLabel = computed(() =>
  homeLang.value === "pl"
    ? "Kod na GitHubie (otwiera nową kartę)"
    : "View source on GitHub (opens in a new tab)",
);

// Show the toggle when either the browser language or the currently persisted
// home-page language is non-English. This ensures users who previously switched
// to a non-English language can always switch back to English, even if their
// browser reports 'en'.
const browserLang = navigator.language.split("-")[0].toLowerCase();
const show = computed(() => browserLang !== "en" || homeLang.value !== "en");

// Show the flag of the currently active home-page language, mirroring
// LanguageToggle.vue (the user sees what is active, not what will activate).
const flag = computed(() => (homeLang.value === "pl" ? "🇵🇱" : "🇬🇧"));
</script>

<style scoped>
.home-header-actions {
  position: absolute;
  top: 16px;
  right: 16px;
  z-index: 10;
  display: flex;
  align-items: center;
  gap: 8px;
}

.home-lang-toggle,
.home-github-link {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 36px;
  height: 36px;
  padding: 0;
  border: 1px solid rgba(167, 139, 250, 0.25);
  border-radius: 10px;
  background: rgba(30, 27, 47, 0.6);
  cursor: pointer;
  transition:
    background 0.15s ease,
    border-color 0.15s ease,
    transform 0.15s ease;
}

.home-lang-toggle:hover {
  background: rgba(60, 50, 95, 0.7);
  border-color: rgba(167, 139, 250, 0.5);
}

.home-github-link {
  color: #a78bfa;
  text-decoration: none;
  box-shadow: 0 0 12px rgba(167, 139, 250, 0.12);
  transition:
    color 0.15s ease,
    background 0.15s ease,
    border-color 0.15s ease,
    box-shadow 0.15s ease;
}

.home-github-link:hover,
.home-github-link:focus-visible {
  color: #ede9fe;
  background: rgba(60, 50, 95, 0.7);
  border-color: #a78bfa;
  box-shadow: 0 0 16px rgba(167, 139, 250, 0.45);
}

.home-github-link:focus-visible,
.home-lang-toggle:focus-visible {
  outline: 2px solid #a78bfa;
  outline-offset: 3px;
}

.home-lang-toggle:active {
  transform: scale(0.96);
}

.home-lang-flag {
  font-size: 18px;
  line-height: 1;
}

@media (max-width: 768px) {
  .home-header-actions {
    position: fixed;
    top: 13px;
    right: 51px;
    left: auto;
  }

  .home-lang-toggle,
  .home-github-link {
    width: 32px;
    height: 32px;
  }
}
</style>
