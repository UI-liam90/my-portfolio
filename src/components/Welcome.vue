<template>
  <div class="welcome-section">
    <h2>
      <span class="rainbow">{{welcomeText()}}</span><br/>
      <span class="rainbow">My Name is Liam</span>
    </h2>
    <h3><span class="rainbow">{{greetingText()}}</span></h3>
  </div>
</template>

<script>
export default {
  name: 'Welcome',
  created () {
    window.addEventListener('scroll', this.handleScroll);
  },
  destroyed () {
    window.removeEventListener('scroll', this.handleScroll);
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
        return 'Good Morning'
      } else if(hour >= 12 && hour < 18) {
        return 'Good Afternoon'
      } else {
        return 'Good evening'
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
    h2 {
      @include rfs(85px, font-size);
      span:nth-of-type(1) {
        animation: load-in 350ms ease-in 500ms 1 normal forwards;
        opacity: 0;
      }
      span:nth-of-type(2) {
        @include rfs(50px, font-size);
        animation: load-in 350ms ease-in 850ms 1 normal forwards;
        opacity: 0;
      }
    }
    h3 {
      @include rfs(40px, font-size);
      animation: load-in 350ms ease-in 1200ms 1 normal forwards;
      opacity: 0;
    }
    span.rainbow {
      --offset: 400px;
      background-image: url(../spectrum.svg);
      background-repeat: repeat-x;
      background-size: 100vw rem-calc(10);
      background-position: left bottom 5px;
      background-position-x: var(--scrollPos);
      padding-bottom: rem-calc(10);
      &:nth-of-type(2) {
        background-position-x: calc(var(--offset) + var(--scrollPos));
      }
    }
  }
    @keyframes load-in {
    from {opacity: 0;}
    to {opacity: 1;}
  }
  
</style>
