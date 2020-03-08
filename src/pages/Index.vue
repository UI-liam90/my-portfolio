<template>
  <Layout>
    <div class="top-grid">
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
        <svg class="bg-icon" style="fill: var(--rainbow-aqua); width: 5vw; top: 20%; left: 50%"><use xlink:href="#icon-circle"></use></svg>
        <svg class="bg-icon" style="fill: var(--rainbow-blue); width: 10vw; top: 80%; left: 80%"><use xlink:href="#icon-square"></use></svg>
        <svg class="bg-icon" style="fill: var(--rainbow-green); width: 12vw; top: 50%; left: 30%"><use xlink:href="#icon-triangle"></use></svg>
      </div>
    </div>
    <div class="about-me">
      <h2>A Little Bit About Me</h2>
      <p>I'm a frontend developer, at least that how I try to market myself... I also have experience using PHP, do basic design work in programs like Photoshop, Illustrator and Figma. I'm not that fabled unicorn (yet) but even after 5 years Industry experience and 3 years Academic experience I'm still willing to get my hands dirty in mirade of web development and also learning and improving.</p>
      <p>My origins started in Norfolk on the east coast of England, but I moved to the North for University and have been living near Manchester ever since. In my free time I like to be the typical nerd. If you're imagining a palesty guy who likes to hangout in a dark and dingly room somewhere, playing that Dugeons & Dragons you've heard of, then you're hitting the ball out of the park :). In addtion to that though I also like to travel, places I have visited in recent years include Florida and Japan, and I hope to visit other location like New Zealand, astralia and Russia when I get the time and resorces to do so.</p>
    </div>
    <div class="portfolio">
      <h4>My most recent work</h4>
      
      <div class="portfolio__items">
        <PortfolioCard v-for="edge in $page.portfolio.edges" :key="edge.node.id" :info="edge.node"/>
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
  // .top-grid {
  //   display: flex;
  //   flex-direction: column;
  //   padding: rem-calc(0 30 50);
  //   @media screen and (min-width: 1024px) {
  //     display: grid;
  //     grid-template-columns: 1fr 1fr;
  //     grid-gap: rem-calc(40);
  //     .welcome {
  //       grid-column: 1 / 2;
  //     }
  //     .portfolio {
  //       grid-column: 2 / 3;
  //     }
  //   }
  //   @media screen and (min-width: 1200px) {
  //     grid-template-columns: 760px 1fr;
  //   } 
  // }
  .welcome-section {
    --offset: 400px;
    position: relative;
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
      &:nth-of-type(2) span {
        @include rfs(55px, font-size);
        animation: load-in 350ms ease-in 850ms 1 normal forwards;
        opacity: 0;
        background-position-x: calc(var(--offset) + var(--scrollPos));
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
  }
    @keyframes load-in {
    from {opacity: 0;}
    to {opacity: 1;}
  }
  .bg-icon {
    position: absolute;
    z-index: 0;
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

