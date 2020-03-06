<template>
  <Layout>
    <div class="top-grid">
      <div class="welcome">
        <Welcome />
      </div>
      <div class="portfolio">
        <PortfolioCard v-for="edge in $page.portfolio.edges" :key="edge.node.id" :info="edge.node"/>
      </div>

    </div>

    <!-- List posts -->
    <div class="posts">
      <PostCard v-for="edge in $page.posts.edges" :key="edge.node.id" :post="edge.node"/>
    </div>

  </Layout>
</template>

<page-query>
query {
  posts: allPost(filter: { published: { eq: true }}) {
    edges {
      node {
        id
        title
        date (format: "D. MMMM YYYY")
        timeToRead
        description
        path
        tags {
          id
          title
          path
        }
      }
    }
  }
  portfolio: allPortfolio(filter: { published: { eq: true }}) {
    edges {
      node {
        id
        title
        date (format: "D. MMMM YYYY")
        timeToRead
        description
        cover_image (width: 660, height: 335, blur: 10)
        path
        tags {
          id
          title
          path
        }
      }
    }
  }
}
</page-query>

<script>
import PostCard from '~/components/PostCard.vue'
import PortfolioCard from '~/components/PortfolioCard.vue'
import Welcome from '~/components/Welcome.vue'

export default {
  components: {
    PostCard,
    PortfolioCard,
    Welcome
  },
  metaInfo: {
    title: 'Hello, world!'
  }
}
</script>

<style lang="scss">
  .top-grid {
    display: flex;
    flex-direction: column;
    @media screen and (min-width: 1024px) {
      display: grid;
      grid-template-columns: 1fr 1fr;
      grid-gap: rem-calc(40);
      .welcome {
        grid-column: 1 / 2;
      }
      .portfolio {
        grid-column: 2 / 3;
      }
    }
    @media screen and (min-width: 1200px) {
      grid-template-columns: 760px 1fr;
    } 
  }
  .portfolio {
    display: flex;
    flex-direction: column;
    @media screen and (min-width: 600px) {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
      grid-gap: rem-calc(30);
      padding: rem-calc(10);
    }
  }
</style>

