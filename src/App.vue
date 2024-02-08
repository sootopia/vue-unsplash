<template>
  <main>
    <SearchForm />
  </main>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import SearchForm from '@/components/search/SearchForm.vue';

export default defineComponent({
  components: {
    SearchForm,
  },
});
</script>
<style lang="scss"></style>
