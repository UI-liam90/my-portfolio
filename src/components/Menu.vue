<template>
  <nav class="main-menu">
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
.main-menu {
    display: none;
  @media screen and (min-width: 850px) {
        display: flex;
        align-items: center;
        padding-right: 50px;
        .menu-link {
            display: flex;
            flex-flow: column nowrap;
            align-items: center;
            justify-content: center;
            padding: 10px 20px;
            font-family: 'Poppins', sans-serif;
            font-weight: 600;
            color: var(--title-color);
            text-decoration: none;
            &:hover {
                text-decoration: underline;
            }
        }
        .icon {
            width: 30px;
            height: 30px;
            fill: var(--title-color)
        }
    }
}
</style>
