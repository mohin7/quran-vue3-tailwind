<script>
// import TheWelcome from '@/components/TheWelcome.vue'
import axios from "axios";
import SuraDetailsVue from "../SuraDetails.vue";
export default {
  data() {
    return {
      surahList: [],
      noOfSurahPerPage: 10,
      currentPage: 1,
    };
  },

  created() {
    this.fetchSurah();
  },
  components: {
    SuraDetailsVue,
  },
  computed: {
    slicedSurah() {
      return this.surahList.slice(
        this.noOfSurahPerPage * (this.currentPage - 1),
        this.noOfSurahPerPage * this.currentPage
      );
    },
  },
  methods: {
    fetchSurah() {
      axios
        .get(
          "https://raw.githubusercontent.com/semarketir/quranjson/master/source/surah.json"
        )
        .then((data) => {
          this.surahList = data.data;
        });
    },
    nextButton() {
      this.currentPage += 1;
    },
    prevButton() {
      this.currentPage -= 1;
    },
  },

  // computed: {
  // },
  // watch: {
  //   nextButton: function (val) {
  //     console.log(val + 1);
  //   },
  // },
};
</script>

<template>
  <tbody>
    <tr
      v-for="(surah, idx) in slicedSurah"
      :key="idx"
      tabindex="0"
      class="focus:outline-none h-10 border border-gray-100 rounded"
    >
      <td>
        <div class="ml-5">{{ surah.index }}</div>
      </td>
      <td>
        <router-link
          :to="{
            name: 'suraDetails',
            params: { id: Math.abs(surah.index) },
          }"
          class=""
        >
          <div class="flex items-center pl-5">
            <p class="text-base font-medium leading-none text-gray-500">
              {{ surah.title }}-({{ surah.titleAr }})
            </p>
          </div>
        </router-link>
      </td>
      <td class="pl-24">
        <div class="flex items-center">
          <p class="text-sm leading-none text-gray-600">
            {{ surah.place }}
          </p>
        </div>
      </td>
      <td class="pl-24">
        <div class="flex items-center">
          <p class="text-sm leading-none text-gray-600">
            {{ surah.type }}
          </p>
        </div>
      </td>
      <td class="pl-5">
        <div class="flex items-center">
          <p class="text-sm leading-none text-gray-600 ml-2">
            {{ surah.count }}
          </p>
        </div>
      </td>

      <td class="pl-4 text-right pr-5">
        <router-link
          :to="{
            name: 'suraDetails',
            params: { id: Math.abs(surah.index) },
          }"
          class="focus:ring-2 focus:ring-offset-2 focus:ring-red-300 text-sm leading-none text-gray-600 py-2 px-5 bg-gray-100 rounded hover:bg-gray-200 focus:outline-none"
        >
          View
        </router-link>
      </td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <td colspan="6">
        <div class="buttons mt-5 flex justify-end w-full">
          <button
            v-show="currentPage > 1"
            @click="prevButton()"
            class="button mr-2"
          >
            Preview
          </button>
          <button
            v-show="currentPage < surahList.length / noOfSurahPerPage"
            @click="nextButton()"
            class="button"
          >
            Next
          </button>
        </div>
      </td>
    </tr>
  </tfoot>
</template>
<style>
.button {
  @apply bg-blue-300 p-2 rounded-sm px-5 hover:bg-blue-700;
}
</style>
