<template>
  <Layout>
    <div class="about-me-section">
      <h2>A Little Bit About Me</h2>
      <p>I'm a frontend developer, at least that how I try to market myself... I also have experience using PHP, do basic design work in programs like Photoshop, Illustrator and Figma. I'm not that fabled unicorn (yet) but even after 5 years Industry experience and 3 years Academic experience I'm still willing to get my hands dirty in mirade of web development and also learning and improving.</p>
      
      <p>My origins started in Norfolk on the east coast of England, but I moved to the North for University and have been living near Manchester ever since. In my free time I like to be the typical nerd. If you are imagining a pasty guy who likes to hang out in a dark and dingy room somewhere, playing that Dungeons & Dragons you've heard of, then you're hitting the ball out of the park :). In addition to that though I also like to travel, places I have visited in recent years include Florida and Japan, and I hope to visit other location like New Zealand, Australia and Russia when I get the time and resources to do so.</p>
    </div>
  </Layout>
</template>


<script>

export default {
  metaInfo: {
    title: 'About Me'
  }
    
}
</script>

<style lang="scss">
  .about-me-section {
    max-width: 1000px;
    margin: 0 auto;
    text-align: left;
    margin-bottom: rem-calc(30);
    @media screen and (min-width: 600px) {
      text-align: center;
      margin-bottom: rem-calc(50);
    }
  }
</style>

