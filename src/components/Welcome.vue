<template>
  <div class="welcome-section">
    <div class="welcome-section__introduction">
      <h2>
        <span class="rainbow">{{welcomeText()}}</span>
      </h2>
      <h2 class="smaller">
        <span class="rainbow">My Name is Liam</span>
      </h2>
      <h3><span class="rainbow">{{greetingText()}}</span></h3>
      <h4>Recent Work</h4>
      <p>Please checkout some of my recent work<span class="recentwork__arrow"></span></p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Welcome',
  mounted() {
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
        return 'Good \n Morning'
      } else if(hour >= 12 && hour < 18) {
        return 'Good \n Afternoon'
      } else {
        return 'Good \n evening'
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
    span.rainbow {
      display: inline;
      background-image: url(../spectrum.svg);
      background-repeat: repeat-x;
      background-size: 100vw rem-calc(10);
      background-position: left bottom 10%;
      background-position-x: var(--scrollPos);
      padding-bottom: rem-calc(10);
    }
    h2 {
      @include rfs(70px, font-size);
      &:nth-of-type(1) span {
        animation: load-in 350ms ease-in 500ms 1 normal forwards;
        opacity: 0;
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
  
</style>
