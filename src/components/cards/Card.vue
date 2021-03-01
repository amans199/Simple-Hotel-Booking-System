<template>
  <b-card
    title="Card Title"
    img-src="https://picsum.photos/600/300/?image=25"
    img-alt="Image"
    img-top
    tag="article"
    class="gap-1em w-50-with-gap"
  >
    <b-card-text>
      Some quick example text to build on the card title and make up the bulk of
      the card's content.
    </b-card-text>

    <b-button href="#" variant="primary">Go somewhere</b-button>
  </b-card>
</template>
<script>
export default {
  //
};
</script>

<style lang="scss" scoped>
.gap-1em {
  margin: 0.5em;
}
.w-50-with-gap {
  width: calc(50% - 1em);
}
</style>