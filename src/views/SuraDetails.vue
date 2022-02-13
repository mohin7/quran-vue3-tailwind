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
          this.surah = data.data;
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
  <main>
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
          <p>Count: {{ surah.count }}</p>
          <p
            tabindex="0"
            class="focus:outline-none text-base sm:text-lg md:text-xl lg:text-2xl font-bold leading-normal text-gray-800"
          >
            Surah Name: ({{ surah.index }})-{{ surah.name }}
          </p>
        </div>
      </div>
      <!-- py-4 md:py-7 px-4 md:px-8 xl:px-10 -->
      <ul>
        <li class="p-3" v-for="(verse, idx) in surah.verse" :key="idx">
          <strong
            class="p-3 bg-blue-200 mr-3 w-12 h-12 inline-block rounded-full leading-12 text-center"
            >{{ idx.slice(6, 9) }} </strong
          >{{ verse }}
        </li>
      </ul>
    </div>
  </main>
</template>

<style>
ul li {
  text-align: right;
}
</style>
