<template>
  <nav class="mobile-menu">
    <g-link class="menu-link" to="/">
    <svg class="icon icon-home"><use xlink:href="#icon-home"></use></svg>
    Home
    </g-link>
    <g-link class="menu-link" to="/#about">
    <svg class="icon icon-smile"><use xlink:href="#icon-smile"></use></svg>
    About
    </g-link>
    <g-link class="menu-link" to="/contact/">
    <svg class="icon icon-mail"><use xlink:href="#icon-mail"></use></svg>
    Contact
    </g-link>
  </nav>
</template>

<static-query>
query {
  metadata {
    siteName
  }
}
</static-query>

<style lang="scss">
.mobile-menu {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding-right: 50px;
    background-color: var(--rainbow-aqua);
    box-shadow: 0px -5px 5px 0px rgba(50, 50, 50, 0.4);
    position: sticky;
    bottom: 0;
    width: 100%;
    z-index: 100;
    padding: 10px 20px;
    .menu-link {
      display: flex;
      flex-flow: column nowrap;
      align-items: center;
      justify-content: center;
      padding: 10px 20px;
      font-family: 'Poppins', sans-serif;
      font-weight: 600;
      color: var(--bg-content-color);
      text-decoration: none;
      &:hover {
          text-decoration: underline;
      }
    }
    .icon {
      width: 20px;
      height: 20px;
      fill: var(--bg-content-color)
    }
    @media screen and (min-width: 850px) {
      display: none;
    }
}
</style>

