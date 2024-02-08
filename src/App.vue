<template>
  <main>
    <section class="search-section py-32">
      <div class="max-w-3xl mx-auto px-5">
        <h1 class="font-semibold text-4xl text-slate-900 text-center mb-10">
          Unsplash Photo Search 🏞️
        </h1>
        <div class="input-group flex">
          <div class="flex-auto">
            <input
              type="text"
              class="w-full h-14 px-5 text-slate-500 border-slate-200 border-solid border rounded-md focus:text-slate-800 focus:border-slate-400 focus:shadow-slate-200 focus:shadow-sm transition-all duration-150 ease-linear outline-none"
              placeholder="검색어를 입력하세요 ..."
              v-model="keyword"
            />
          </div>
          <div class="ps-2">
            <button
              class="h-full px-4 rounded-md bg-teal-600 hover:bg-teal-700 text-white font-medium"
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
        <div class="result-wrapper columns-4 gap-8">
          <div class="result-card mb-8">
            <figure class="result__card--thumbnail">
              <a href="#none" class="block">
                <img src="//dummyimage.com/480x720" alt="" loading="lazy" />
              </a>
            </figure>
          </div>

          <div class="result-card mb-8">
            <figure class="result__card--thumbnail">
              <a href="#none" class="block">
                <img src="//dummyimage.com/480x320" alt="" loading="lazy" />
              </a>
            </figure>
          </div>

          <div class="result-card mb-8">
            <figure class="result__card--thumbnail">
              <a href="#none" class="block">
                <img src="//dummyimage.com/480x960" alt="" loading="lazy" />
              </a>
            </figure>
          </div>

          <div class="result-card mb-8">
            <figure class="result__card--thumbnail">
              <a href="#none" class="block">
                <img src="//dummyimage.com/480x560" alt="" loading="lazy" />
              </a>
            </figure>
          </div>

          <div class="result-card mb-8">
            <figure class="result__card--thumbnail">
              <a href="#none" class="block">
                <img src="//dummyimage.com/480x480" alt="" loading="lazy" />
              </a>
            </figure>
          </div>

          <div class="result-card mb-8">
            <figure class="result__card--thumbnail">
              <a href="#none" class="block">
                <img src="//dummyimage.com/480x320" alt="" loading="lazy" />
              </a>
            </figure>
          </div>

          <div class="result-card mb-8">
            <figure class="result__card--thumbnail">
              <a href="#none" class="block">
                <img src="//dummyimage.com/480x720" alt="" loading="lazy" />
              </a>
            </figure>
          </div>

          <div class="result-card mb-8">
            <figure class="result__card--thumbnail">
              <a href="#none" class="block">
                <img src="//dummyimage.com/480x640" alt="" loading="lazy" />
              </a>
            </figure>
          </div>
        </div>
      </div>
    </section>
  </main>
</template>

<script lang="ts">
import { createApi } from 'unsplash-js';

const unsplash = await createApi({
  accessKey: '2YpEaaopXWtfjQyRH85ucF1dvO8T6pcxErpvgm3P7fY',
});

export default {
  // setup() {},
  data() {
    return {
      keyword: '',
      resultItems: {},
      currentPage: 1,
    };
  },
  methods: {
    async getImages() {
      try {
        const res = await unsplash.search.getPhotos({
          query: this.keyword,
          perPage: 20,
        });

        if (res.status === 200) {
          this.resultItems = res.response ? res.response.results : {};
        }
      } catch (error) {
        alert('오류가 발생했어요.');
      }
    },
  },
};
</script>
<style lang="scss">
p {
  font-size: 20px;
}
</style>
