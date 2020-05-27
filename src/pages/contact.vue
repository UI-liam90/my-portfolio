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
      @include rfs(75px, font-size);
      color: var(--rainbow-orange);
      transition: all 350ms ease;
      text-decoration: none;
      &:hover {
        color: var(--rainbow-aqua);
      }
    }
  }
</style>

