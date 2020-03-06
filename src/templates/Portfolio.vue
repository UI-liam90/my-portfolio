<template>
  <Layout>
    {{ $page.portfolio.title }}

  </Layout>
</template>

<script>

export default {
  metaInfo () {
    return {
      title: this.$page.portfolio.title,
      meta: [
        {
          name: 'description',
          content: this.$page.portfolio.description
        }
      ]
    }
  }
}
</script>

<page-query>
query Portfolio ($id: ID!) {
  portfolio (id: $id) {
    title
  }
}
</page-query>

<style lang="scss">
.portfolio-title {
  padding: calc(var(--space) / 2) 0 calc(var(--space) / 2);
  text-align: center;
}

.portfolio {

  &__header {
    width: calc(100% + var(--space) * 2);
    margin-left: calc(var(--space) * -1);
    margin-top: calc(var(--space) * -1);
    margin-bottom: calc(var(--space) / 2);
    overflow: hidden;
    border-radius: var(--radius) var(--radius) 0 0;

    img {
      width: 100%;
    }

    &:empty {
      display: none;
    }
  }

  &__content {
    h2:first-child {
      margin-top: 0;
    }

    p:first-of-type {
      font-size: 1.2em;
      color: var(--title-color);
    }

    img {
      width: calc(100% + var(--space) * 2);
      margin-left: calc(var(--space) * -1);
      display: block;
      max-width: none;
    }
  }
}

.portfolio-comments {
  padding: calc(var(--space) / 2);

  &:empty {
    display: none;
  }
}

.portfolio-author {
  margin-top: calc(var(--space) / 2);
}
</style>
