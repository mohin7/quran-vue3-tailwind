<script>
// import TheWelcome from '@/components/TheWelcome.vue'
import axios from "axios";
import SuraDetailsVue from "../SuraDetails.vue";
export default {
  data() {
    return {
      madaniyah: [],
      currentPage: 1,
      noOfSurahPerPage: 10,
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
      return this.madaniyah.slice(
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
          const allSurah = data.data;

          // console.log(data.data);
          allSurah.filter((el) => {
            if (el.type === "Madaniyah") {
              setTimeout(() => {
                this.madaniyah.push(el);
              }, 500);
              //   console.log(this.madaniyah);
            }
          });
        });
    },
    nextButton() {
      this.currentPage += 1;
    },
    prevButton() {
      this.currentPage -= 1;
    },
  },
};
</script>

<template>
  <tbody v-if="madaniyah.length > 0">
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

  <div
    v-else
    class="w-full h-full fixed block top-0 left-0 bg-white opacity-75 z-50"
  >
    <span
      class="text-green-500 opacity-75 top-1/2 my-0 mx-auto block relative w-0 h-0"
      style="top: 50%"
    >
      <i class="fas fa-circle-notch fa-spin fa-5x"></i>
    </span>
  </div>
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
            v-show="currentPage < madaniyah.length / noOfSurahPerPage"
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
