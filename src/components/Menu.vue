<template>
    <Bubble noOverlay>
      <g-link to="/">Welcome</g-link>
      <g-link to="/about/">About Me</g-link>
    </Bubble>
</template>

<script>

import { Bubble } from 'vue-burger-menu'  // import the CSS transitions you wish to use, in this case we are using `Slide`

export default {
    components: {
        Bubble // Register your component
    }
}
</script>