<template>
  <div class="portfolio-card">
    <div class="portfolio-card__header">
      <g-image alt="Cover image" v-if="info.cover_image" class="portfolio-card__image" :src="info.cover_image" />
    </div>
    <div class="portfolio-card__content" :data-micromodal-trigger="info.id">
      <h2 class="portfolio-card__title" v-html="info.title" />
      <a class="portfolio-card__link">Read More</a>
    </div>
  </div>
</template>

<script>

export default {
  props: ['info'],
}
</script>

<style lang="scss">
  .portfolio-card {
    --space: rem-calc(30);
    margin-bottom: rem-calc(30);
    position: relative;
    background-color: var(--bg-content-color);
    overflow: hidden;
    border-radius: 5px 30px 5px 30px;
    box-shadow: 10px 10px 0px 0px #5461c8;
    .portfolio-card__image {
      margin-left: calc(var(--space) * -1);
      margin-right: calc(var(--space) * -1);
      margin-bottom: calc(var(--space) / 2);
      margin-top: calc(var(--space) * -1);
    }
    .portfolio-card__content {
      padding: rem-calc(15);
    }
    .portfolio-card__link {
      display: inline-block;
      background-color: var(--rainbow-aqua);
      color: var(--bg-content-color);
      padding: rem-calc(5 15);
      border-radius: rem-calc(30);
      border: 2px solid var(--rainbow-aqua);
      transition: all 250ms ease-in-out;
      cursor: pointer;
      &:hover, &:focus {
        background: transparent;
        color: var(--rainbow-aqua);
      }
    }
    &:nth-of-type(2n+2) {
      box-shadow: 10px 10px 0px 0px var(--rainbow-pink);
    }
    &:nth-of-type(3n+3) {
      box-shadow: 10px 10px 0px 0px var(--rainbow-red);
    }
    &:nth-of-type(4n+4) {
      box-shadow: 10px 10px 0px 0px var(--rainbow-orange);
    }
    &:nth-of-type(5n+5) {
      box-shadow: 10px 10px 0px 0px var(--rainbow-yellow);
    }
    &:nth-of-type(6n+6) {
      box-shadow: 10px 10px 0px 0px var(--rainbow-green);
    }
    &:nth-of-type(7n+7) {
      box-shadow: 10px 10px 0px 0px var(--rainbow-aqua);
    }
    &:nth-of-type(8n+8) {
      box-shadow: 10px 10px 0px 0px var(--rainbow-blue);
    }
  }
</style>
