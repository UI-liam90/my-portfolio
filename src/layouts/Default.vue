<template>
  <div id="app">

    <header class="header">
      <div class="header__left">
        <Logo v-if="showLogo" /> 
      </div>
      
      <div class="header__right">        
        <ToggleTheme />
      </div>
    </header>

    <main class="main">
      <slot/>
    </main>

    <footer class="footer">
      <span class="footer__copyright">Copyright © {{ new Date().getFullYear() }}. </span>
      <span class="footer__links">Powered by <a href="//gridsome.org"> Gridsome </a></span>
    </footer>
    <svg aria-hidden="true" style="position: absolute; width: 0; height: 0; overflow: hidden;" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
      <defs>
      <symbol id="icon-circle" viewBox="0 0 32 32">
      <title>oval</title>
      <path d="M16 32c-8.822 0-16-7.178-16-16s7.178-16 16-16 16 7.178 16 16-7.178 16-16 16zM16 4c-6.617 0-12 5.383-12 12s5.383 12 12 12 12-5.383 12-12-5.383-12-12-12z"></path>
      </symbol>
      <symbol id="icon-triangle" viewBox="0 0 32 32">
      <title>triangle</title>
      <path d="M31.601 25.548l-13.251-21.935c-1.073-1.788-3.659-1.781-4.727-0.002l-13.225 21.937c-0 0.001-0.001 0.001-0.001 0.002-1.103 1.838 0.219 4.175 2.364 4.175h26.477c2.142-0 3.469-2.333 2.363-4.178zM29.238 27.851h-26.477c-0.685 0-1.109-0.746-0.757-1.334l13.226-21.939c0.341-0.569 1.168-0.574 1.514 0.002l13.251 21.935c0.353 0.588-0.070 1.336-0.756 1.336z"></path>
      </symbol>
      <symbol id="icon-square" viewBox="0 0 32 32">
      <title>square</title>
      <path d="M28.25 0h-24.5c-2.068 0-3.75 1.682-3.75 3.75v24.5c0 2.068 1.682 3.75 3.75 3.75h24.5c2.068 0 3.75-1.682 3.75-3.75v-24.5c0-2.068-1.682-3.75-3.75-3.75zM29.5 28.25c0 0.689-0.561 1.25-1.25 1.25h-24.5c-0.689 0-1.25-0.561-1.25-1.25v-24.5c0-0.689 0.561-1.25 1.25-1.25h24.5c0.689 0 1.25 0.561 1.25 1.25v24.5z"></path>
      </symbol>
      </defs>
    </svg>
  </div>
</template>

<script>
import Logo from '~/components/Logo.vue'
import ToggleTheme from '~/components/ToggleTheme.vue'

export default {
  props: {
    showLogo: { default: true }
  },
  components: {
    Logo,
    ToggleTheme
  }
}
</script>

<style lang="scss">
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  min-height: var(--header-height);
  padding: 0 rem-calc(30);
  top:0;
  z-index: 10;
  background: var(--bg-color);
  &__left,
  &__right {
    display: flex;
    align-items: center;
  }

  @media screen and (min-width: 1300px) {
    //Make header sticky for large screens
    position: sticky;
    width: 100%;
    z-index: 100;
  }
}

.main {
  margin: 0 auto;
  padding: 1.5vw 15px 0;
}

.footer {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: calc(var(--space) / 2);
  text-align: center;
  font-size: .8em;

  > span {
    margin: 0 .35em;
  }

  a {
    color: currentColor;
  }
}
</style>
