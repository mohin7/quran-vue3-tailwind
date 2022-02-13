<script>
// import TheWelcome from '@/components/TheWelcome.vue'
import axios from "axios";
import AllSurahVue from "./surah-tabs/AllSurah.vue";
import Madaniyah from "./surah-tabs/Madaniyah.vue";
import Makkiya from "./surah-tabs/Makkiya.vue";

export default {
  data() {
    return {
      surahList: [],
      makkiyah: [],
      madaniyah: [],

      currentCom: "AllSurahVue",
    };
  },
  created() {
    this.fetchSurah();
  },
  components: {
    AllSurahVue,
    Makkiya,
    Madaniyah,
  },
  methods: {
    fetchSurah() {
      axios
        .get(
          "https://raw.githubusercontent.com/semarketir/quranjson/master/source/surah.json"
        )
        .then((data) => {
          this.surahList = data.data;
          // console.log(data.data);
          this.surahList.filter((el) => {
            if (el.type === "Makkiyah") {
              this.makkiyah.push(el);
            } else {
              this.madaniyah.push(el);
            }
          });
        });
    },
  },
};
</script>

<template>
  <main>
    <div class="container mx-auto mb-5">
      <!--- more free and premium Tailwind CSS components at https://tailwinduikit.com/ --->

      <div class="py-4 md:py-7">
        <div class="flex items-center justify-between">
          <p
            tabindex="0"
            class="focus:outline-none text-base sm:text-lg md:text-xl lg:text-2xl font-bold leading-normal text-gray-800"
          >
            Surah List
          </p>
          <div
            class="py-3 px-4 flex items-center text-sm font-medium leading-none text-gray-600 bg-gray-200 hover:bg-gray-300 cursor-pointer rounded"
          >
            <p>Sort By:</p>
            <select
              aria-label="select"
              class="focus:text-indigo-600 focus:outline-none bg-transparent ml-1"
            >
              <option class="text-sm text-indigo-800">Latest</option>
              <option class="text-sm text-indigo-800">Oldest</option>
              <option class="text-sm text-indigo-800">Latest</option>
            </select>
          </div>
        </div>
      </div>
      <!-- py-4 md:py-7 px-4 md:px-8 xl:px-10 -->
      <div class="bg-white">
        <div class="sm:flex items-center justify-between">
          <div class="flex items-center">
            <a
              @click="currentCom = 'AllSurahVue'"
              class="cursor-pointer rounded-full focus:outline-none focus:ring-2 focus:bg-indigo-50 focus:ring-indigo-800"
            >
              <div
                :class="[
                  currentCom == 'AllSurahVue'
                    ? 'bg-indigo-100 text-indigo-700'
                    : 'text-gray-600',
                ]"
                class="py-2 px-8 rounded-full"
              >
                <p>All</p>
              </div>
            </a>
            <a
              @click="currentCom = 'Makkiya'"
              class="cursor-pointer rounded-full focus:outline-none focus:ring-2 focus:bg-indigo-50 focus:ring-indigo-800 ml-4 sm:ml-8"
            >
              <div
                :class="[
                  currentCom == 'Makkiya'
                    ? 'bg-indigo-100 text-indigo-700'
                    : 'text-gray-600',
                ]"
                class="py-2 px-8 text-gray-600 hover:text-indigo-700 hover:bg-indigo-100 rounded-full"
              >
                <p>Makkiyah</p>
              </div>
            </a>
            <a
              @click="currentCom = 'Madaniyah'"
              class="cursor-pointer rounded-full focus:outline-none focus:ring-2 focus:bg-indigo-50 focus:ring-indigo-800 ml-4 sm:ml-8"
            >
              <div
                :class="[
                  currentCom == 'Madaniyah'
                    ? 'bg-indigo-100 text-indigo-700'
                    : 'text-gray-600',
                ]"
                class="py-2 px-8 text-gray-600 hover:text-indigo-700 hover:bg-indigo-100 rounded-full"
              >
                <p>Madaniyah</p>
              </div>
            </a>
          </div>
          <button
            onclick="popuphandler(true)"
            class="focus:ring-2 focus:ring-offset-2 focus:ring-indigo-600 mt-4 sm:mt-0 inline-flex items-start justify-start px-6 py-3 bg-indigo-700 hover:bg-indigo-600 focus:outline-none rounded"
          >
            <p class="text-sm font-medium leading-none text-white">Add Task</p>
          </button>
        </div>
        <div class="mt-7 overflow-x-auto">
          <table class="w-full whitespace-nowrap">
            <thead>
              <tr
                tabindex="0"
                class="focus:outline-none h-10 border border-gray-100 rounded"
              >
                <td>
                  <div class="ml-5">#NO</div>
                </td>
                <td class="">
                  <div class="flex items-center pl-5">
                    <p
                      class="text-base font-medium leading-none text-gray-700 mr-2"
                    >
                      Surah Name
                    </p>
                  </div>
                </td>
                <td class="pl-24">
                  <div class="flex items-center">
                    <p
                      class="text-base font-medium leading-none text-gray-700 mr-2"
                    >
                      Place
                    </p>
                  </div>
                </td>
                <td class="pl-24">
                  <div class="flex items-center">
                    <p
                      class="text-base font-medium leading-none text-gray-700 mr-2"
                    >
                      Type
                    </p>
                  </div>
                </td>
                <td class="pl-5">
                  <div class="flex items-center">
                    <p
                      class="text-base font-medium leading-none text-gray-700 mr-2"
                    >
                      Count
                    </p>
                  </div>
                </td>

                <td class="pl-4 text-right pr-5">Action</td>
              </tr>
            </thead>
            <transition name="fade">
              <keep-alive>
                <component :is="currentCom"></component>
              </keep-alive>
            </transition>
          </table>
        </div>
      </div>
    </div>
  </main>
</template>
<style>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
