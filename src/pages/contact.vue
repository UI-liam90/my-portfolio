<template>
  <Layout>
    <div class="contact-me">
      <div class="container">
        <a href="mailto:hello@liamwebwright.co.uk" class="large-link">hello@liamwebwright.co.uk</a>
        <p>(It doesn't need to be complicated with forms and all that jazz.... just send me a message)</p>
      </div>
    </div>
  </Layout>
</template>


<script>

export default {
  metaInfo: {
    title: 'Contact'
  }
    
}
</script>

<style lang="scss">
  .contact-me {
    text-align: center;
    display: flex;
    align-items: center;
    min-height: 75vh;
    a {
      font-family: 'Luckiest Guy', cursive;
      @include rfs(30px, font-size);
      color: var(--rainbow-orange);
      transition: all 350ms ease;
      text-decoration: none;
      word-break: break-all;
      &:hover {
        color: var(--rainbow-aqua);
      }
      @media screen and (min-width: 500px){
        @include rfs(45px, font-size);
      }
      @media screen and (min-width: 800px){
        @include rfs(70px, font-size);
      }
    }
    p {
      font-size: rem-calc(12);
      @media screen and (min-width: 500px){
        @include rfs(16px, font-size);
      }
    }
  }
</style>

