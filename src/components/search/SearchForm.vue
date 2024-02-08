<template>
  <div>
    <section class="search-section py-32">
      <div class="max-w-3xl mx-auto px-5">
        <h1 class="font-semibold text-4xl text-slate-900 text-center mb-10">
          Unsplash Photo Search 🏞️
        </h1>
        <div class="input-group flex">
          <div class="flex-auto">
            <input
              type="text"
              class="w-full h-14 px-5 text-slate-500 border-slate-200 border-solid border rounded-xl focus:text-slate-800 focus:border-blue-500 focus:shadow-blue-500 focus:shadow-[0_0_0_1px] transition-all duration-150 ease-linear outline-none"
              :class="{
                'text-red-500 border-red-500 shadow-red-500 shadow-[0_0_0_1px]':
                  keywordHasError,
              }"
              placeholder="검색어를 입력하세요 ..."
              v-model="keyword"
              @input="checkKeyword"
              @keyup.enter="getImages"
              required
            />
          </div>
          <div class="ps-2">
            <button
              class="h-full px-6 rounded-xl bg-blue-500 active:opacity-70 transition-opacity duration-100 text-white font-medium outline-0"
              @click="getImages"
            >
              검색
            </button>
          </div>
        </div>
      </div>
    </section>

    <section class="search-result pb-32">
      <div class="container mx-auto px-5">
        <div class="result-wrapper columns-4 gap-6">
          <ResultItem
            v-if="resultItems.length > 1"
            v-for="(item, i) of resultItems"
            :key="i"
            :data="item"
          />
        </div>
      </div>
    </section>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { createApi } from 'unsplash-js';
import ResultItem from '@/components/search/ResultItem.vue';

const unsplash = await createApi({
  accessKey: '2YpEaaopXWtfjQyRH85ucF1dvO8T6pcxErpvgm3P7fY',
});

export default defineComponent({
  components: {
    ResultItem,
  },
  data() {
    return {
      keyword: '',
      resultItems: [{}],
      currentPage: 1,
      keywordHasError: false,
      formIsValid: false,
    };
  },
  computed: {},
  methods: {
    checkKeyword() {
      this.keywordHasError = this.keyword.replace(/\s/gi, '').length < 1;
      this.updateFormValidaty();
    },
    updateFormValidaty() {
      this.formIsValid = !this.keywordHasError;
    },
    async getImages() {
      if (this.keywordHasError || !this.formIsValid) return;

      try {
        const res = await unsplash.search.getPhotos({
          query: this.keyword,
          perPage: 20,
        });

        if (res.status === 200) {
          this.resultItems = res.response?.results ? res.response.results : [];
          this.currentPage = 1;
          console.log(this.resultItems);
        }
      } catch (error) {
        alert('오류가 발생했어요.');
      }
    },
    async loadMore() {
      // if (this.keywordHasError || !this.formIsValid) return;

      try {
        const res = await unsplash.search.getPhotos({
          query: this.keyword,
          perPage: 20,
          page: this.currentPage,
        });

        if (res.status === 200) {
          res.response?.results.forEach(item => {
            this.resultItems.push(item);
          });

          this.currentPage++;
        }
      } catch (error) {
        alert('오류가 발생했어요.');
      }
    },
  },
});
</script>

<style lang="scss" scoped></style>
