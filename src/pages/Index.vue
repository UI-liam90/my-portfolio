<template>
  <Layout>
    <div class="top-grid">
      <div class="welcome">
        <Welcome />
      </div>
      <div class="portfolio">
        <div class="portfolio__items">
          <PortfolioCard v-for="edge in $page.portfolio.edges" :key="edge.node.id" :info="edge.node"/>
        </div>
      </div>
    </div>
    <div class="about-me">
      <h2>A Little Bit About Me</h2>
      <p>I'm a frontend developer, at least that how I try to market myself... I also have experience using PHP, do basic design work in programs like Photoshop, Illustrator and Figma. I'm not that fabled unicorn (yet) but even after 5 years Industry experience and 3 years Academic experience I'm still willing to get my hands dirty in mirade of web development and also learning and improving.</p>
      <p>My origins started in Norfolk on the east coast of England, but I moved to the North for University and have been living near Manchester ever since. In my free time I like to be the typical nerd. If you're imagining a palesty guy who likes to hangout in a dark and dingly room somewhere, playing that Dugeons & Dragons you've heard of, then you're hitting the ball out of the park :). In addtion to that though I also like to travel, places I have visited in recent years include Florida and Japan, and I hope to visit other location like New Zealand, astralia and Russia when I get the time and resorces to do so.</p>
    </div>
    <!-- List posts -->
    <div class="posts">
      <PostCard v-for="edge in $page.posts.edges" :key="edge.node.id" :post="edge.node"/>
    </div>
    <Modal v-for="edge in $page.portfolio.edges" :key="edge.node.id" :info="edge.node"/>
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
  portfolio: allPortfolio(filter: { published: { eq: true }}, limit: 2) {
    edges {
      node {
        id
        title
        date (format: "D. MMMM YYYY")
        timeToRead
        description
        cover_image (width: 660, height: 335, blur: 10)
        path
        content
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
import Modal from '~/components/Modal.vue'
import MicroModal from 'micromodal'; 

export default {
  components: {
    PostCard,
    PortfolioCard,
    Welcome,
    Modal
  },
  metaInfo: {
    title: 'Hello, world!'
  },
  mounted() {
    MicroModal.init();
  }
}
</script>

<style lang="scss">
  .top-grid {
    display: flex;
    flex-direction: column;
    padding: rem-calc(0 30 50);
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
  .portfolio__items {
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

