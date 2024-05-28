<template>
  <div class="character-card">
    <img :src="character.image" :alt="character.name" />
    <h2>{{ character.name }}</h2>
    <p>Status: {{ character.status }}</p>
    <p>Species: {{ character.species }}</p>
  </div>
</template>

<script>
export default {
  props: {
    character: Object,
  },
};
</script>
