<script>
// import TheWelcome from '@/components/TheWelcome.vue'
import axios from "axios";
import { mixin } from "../mixins/mixins";
export default {
  data() {
    return {
      surah: [],
    };
  },
  created() {
    this.fetchSingleSurah();
  },
  methods: {
    fetchSingleSurah() {
      axios
        .get(
          `https://raw.githubusercontent.com/semarketir/quranjson/master/source/surah/surah_${this.loadedID}.json`
        )
        .then((data) => {
          setTimeout(() => {
            this.surah = data.data;
          }, 200);
        });
    },
    backToHome() {
      this.$router.push("/");
    },
  },
  mixins: [mixin],
};
</script>

<template>
  <main v-if="surah.verse">
    <div class="container mx-auto mb-5">
      <!--- more free and premium Tailwind CSS components at https://tailwinduikit.com/ --->
      <div class="py-4 md:py-7">
        <div class="flex items-center justify-between">
          <button
            @click="backToHome"
            class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
          >
            Back
          </button>
          <p>
            Total Count: <strong>{{ surah.count }}</strong>
          </p>
          <p>
            Surah No:# <strong>{{ surah.index }}</strong>
          </p>
          <p
            tabindex="0"
            class="focus:outline-none text-base sm:text-lg md:text-xl lg:text-xl font-bold leading-normal text-gray-800"
          >
            Surah Name: {{ surah.name }}
          </p>
        </div>
      </div>
      <!-- py-4 md:py-7 px-4 md:px-8 xl:px-10 -->
      <ul>
        <li class="p-3" v-for="(verse, idx) in surah.verse" :key="idx">
          <strong
            class="bg-blue-100 font-normal mr-3 w-8 h-8 inline-block rounded-full leading-8 text-center text-xs"
            >{{ idx.slice(6, 9) }} </strong
          >{{ verse }}
        </li>
      </ul>
    </div>
  </main>
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
</template>

<style scoped>
main {
  min-height: calc(100vh - 400px);
}
ul li {
  text-align: right;
}
</style>
