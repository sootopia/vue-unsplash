<template>
  <div class="result-card mb-6">
    <figure class="result__card--thumbnail">
      <a href="#none" class="block">
        <img
          class="w-full"
          :src="data?.urls.thumb"
          alt="data?.alt_description"
          loading="lazy"
        />
      </a>
    </figure>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  props: {
    data: Object,
  },
  setup() {
    return {};
  },
});
</script>

<style scoped></style>
