<script lang="ts" setup>
import { isDark } from '../../composables/dark'
import { useLang } from '../../composables/lang'
import { sponsors } from '../../../config/sponsors'

import SponsorsButton from '../sponsors/sponsors-button.vue'

const lang = useLang()

const langZhCN = 'zh-CN'

const getSponsorName = (sponsor) => {
  if (lang.value === langZhCN) {
    return sponsor.name_cn || sponsor.name
  }
  return sponsor.name
}
const getSponsorSlogan = (sponsor) => {
  if (lang.value === langZhCN) {
    return sponsor.slogan_cn || sponsor.slogan
  }
  return sponsor.slogan
}
</script>

<template>
  <div class="sponsors-container" m="t-9 auto">
    <div class="sponsors-list">
      <a
        v-for="(sponsor, i) in sponsors"
        :key="i"
        :class="['sponsor', sponsor.className]"
        :href="sponsor.url"
        target="_blank"
      >
        <img
          :class="sponsor.isDark && isDark ? 'filter invert' : ''"
          width="45"
          :src="sponsor.img"
          :alt="sponsor.name"
        />
        <div>
          <p>
            Sponsored by
            <span class="name">{{ getSponsorName(sponsor) }}</span>
          </p>
          <p>{{ getSponsorSlogan(sponsor) }}</p>
        </div>
      </a>
    </div>
    <sponsors-button round />
  </div>
</template>

<style lang="scss">
.home-page {
  .sponsors-container {
    width: 92%;
    .join {
      text-align: center;
      margin: 0 0 50px 0;
    }
  }

  .sponsors-list {
    display: flex;
    justify-content: center;
  }

  .sponsor {
    margin: 0 20px 10px;
    display: inline-flex;
    width: 300px;
    height: 100px;
    justify-content: center;
    align-items: center;

    .name {
      font-weight: bold;
      color: var(--text-color);
    }

    img {
      margin-right: 20px;
    }

    div {
      display: flex;
      flex-direction: column;
      justify-content: center;
    }

    p {
      margin: 0;
      line-height: 1.8;
      color: var(--text-color-light);
      font-size: 12px;
    }
  }
}
</style>
