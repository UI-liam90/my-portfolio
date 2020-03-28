<template>
  <Layout>
    <div class="hero">
      <div class="welcome-section">
        <div class="welcome-section__introduction">
          <h2>
            <span class="rainbow" v-html="welcomeText()"/>
          </h2>
          <h2 class="smaller">
            <span class="rainbow">My Name is Liam</span>
          </h2>
          <h3><span class="rainbow">{{greetingText()}}</span></h3>
        </div>
      </div>
      <svg class="bg-icon bg-icon--one"><use xlink:href="#icon-circle"></use></svg>
      <svg class="bg-icon bg-icon--two"><use xlink:href="#icon-square"></use></svg>
      <svg class="bg-icon bg-icon--three"><use xlink:href="#icon-triangle"></use></svg>
    </div>

    <div class="portfolio">
      <h3>Checkout some of my recent work</h3>
      
      <div class="portfolio__items">
        <PortfolioCard v-for="edge in $page.portfolio.edges" :key="edge.node.id" :info="edge.node"/>
      </div>
    </div>

    <div class="glide">
      <div class="glide__track" data-glide-el="track">
        <div class="glide__slides">
          <PortfolioCard v-for="edge in $page.portfolio.edges" :key="edge.node.id" :info="edge.node"/>
        </div>
      </div>
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
  portfolio: allPortfolio(filter: { published: { eq: true }}, limit: 4) {
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
import Modal from '~/components/Modal.vue'
import MicroModal from 'micromodal';
import Glide from '@glidejs/glide';

export default {
  components: {
    PostCard,
    PortfolioCard,
    Modal
  },
  metaInfo: {
    title: 'Welcome'
  },
  mounted() {
    MicroModal.init();
    window.addEventListener('scroll', this.handleScroll);
    var portfolioSlider = new Glide('.glide', {
      type: "slider",
      perView: 2,
      gap: 20,
      autoplay: 2000,
      peek: 30,
      breakpoints: {
        500: {
          perView: 1,
        }
      }
    });
    function sliderInit(x) {
      if (x.matches) { // If media query matches
        portfolioSlider.mount();
      } else {
        portfolioSlider.destroy();
      }
    }

    var x = window.matchMedia("(max-width: 680px)")
    sliderInit(x);
    x.addListener(sliderInit);
  },
  methods: {
    handleScroll (event) {
      let scrollTop = document.body.scrollTop ? document.body.scrollTop : document.documentElement.scrollTop; 
      let newPos = scrollTop + "px";
      document.documentElement.style.setProperty('--scrollPos', newPos);
    },
    welcomeText: ()=> {
      let time = new Date();
      let hour = time.getHours();
      if(hour >= 0 && hour < 12) {
        return `
        Good 
        Morning`
      } else if(hour >= 12 && hour < 18) {
        return `
        Good
        Afternoon`
      } else {
        return `
        Good
        evening`
      }
    },
    greetingText: ()=> {
      const greetings = [
        'How are you Today?',
        'I hope you are having a great day :)',
        'How can I help you on this fine day?'
      ];
      return greetings[Math.floor(Math.random() * greetings.length)];
    }
  }
}
</script>

<style lang="scss">
  .welcome-section {
    --offset: 400px;
    text-align: left;
    @media screen and (min-width: 600px) {
      text-align: center;
    }
    > * {
      position: relative;
      z-index: 10;
    }
    span.rainbow {
      display: inline;
      background-image: url(../spectrum.svg);
      background-repeat: repeat-x;
      background-size: 100vw 0.2em;
      background-position: left bottom 10%;
      background-position-x: var(--scrollPos);
      padding-bottom: rem-calc(10);
    }
    h2 {
      @include rfs(100px, font-size);
      &:nth-of-type(1) span {
        animation: load-in 350ms ease-in 500ms 1 normal forwards;
        opacity: 0;
      }
      &:nth-of-type(2) {
        margin-bottom: 50px;
      }
      &:nth-of-type(2) span, &.smaller span {
        @include rfs(55px, font-size);
        animation: load-in 350ms ease-in 850ms 1 normal forwards;
        opacity: 0;
        background-position-x: calc(400px + var(--scrollPos));
      }
    }
    h3 {
      @include rfs(40px, font-size);
      animation: load-in 350ms ease-in 1200ms 1 normal forwards;
      opacity: 0;
      line-height: 1.6;
    }
    .welcome-section__introduction {
      margin-bottom: rem-calc(40);
    }
    h4 {
      @include rfs(30px, font-size);
    }
    .bg-icon {
      position: absolute;
      transition: all 250ms ease;
    }
  }
  .hero {
    position: relative;
    .bg-icon {
      position: absolute;
      z-index: -1;
    }
    .bg-icon--one {
      fill: var(--rainbow-aqua); 
      min-width: rem-calc(30);
      width: 5vw; 
      max-width: rem-calc(90);
      top: 5%; 
      left: 90%;
      animation: rainbow-one 20s ease-in 0s infinite alternate both;
    }
    .bg-icon--two {
      fill: var(--rainbow-blue); 
      min-width: rem-calc(25);
      width: 4vw; 
      max-width: rem-calc(100);
      top: 80%; 
      left: 75%;
      animation: rainbow-two 20s ease-in 15s infinite alternate both;
      transform: rotate(105deg);
    }
    .bg-icon--three {
      fill: var(--rainbow-green); 
      min-width: rem-calc(45);
      width: 6vw; 
      max-width: rem-calc(120);
      top: 40%; 
      left: 10%;
      animation: rainbow-three 20s ease-in 25s infinite alternate both;
      transform: rotate(45deg);
    }
  }
  .portfolio__items {
    display: none;
    @media screen and (min-width: 680px) {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
      grid-gap: rem-calc(30);
      padding: rem-calc(10);
      max-width: rem-calc(1590);
    }
  }
  .glide {
    display: block;
    .glide__slides {
      padding-right: rem-calc(30);
    }
    @media screen and (min-width: 680px) {
      display: none;
    }
  }
</style>

