<script>
// import TheWelcome from '@/components/TheWelcome.vue'
import axios from "axios";
import SuraDetailsVue from "./SuraDetails.vue";
export default {
  data() {
    return {
      surahList: [],
      makkiyah: [],
      madaniyah: [],
    };
  },
  created() {
    this.fetchSurah();
  },
  components: {
    SuraDetailsVue,
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
              console.log(this.makkiyah);
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
              class="rounded-full focus:outline-none focus:ring-2 focus:bg-indigo-50 focus:ring-indigo-800"
              href=" javascript:void(0)"
            >
              <div class="py-2 px-8 bg-indigo-100 text-indigo-700 rounded-full">
                <p>All</p>
              </div>
            </a>
            <a
              class="rounded-full focus:outline-none focus:ring-2 focus:bg-indigo-50 focus:ring-indigo-800 ml-4 sm:ml-8"
            >
              <div
                class="py-2 px-8 text-gray-600 hover:text-indigo-700 hover:bg-indigo-100 rounded-full"
              >
                <p>Makkiyah</p>
              </div>
            </a>
            <a
              class="rounded-full focus:outline-none focus:ring-2 focus:bg-indigo-50 focus:ring-indigo-800 ml-4 sm:ml-8"
            >
              <div
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
            <tbody v-for="(surah, idx) in surahList" :key="idx">
              <tr
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
                      <p
                        class="text-base font-medium leading-none text-gray-500"
                      >
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
          </table>
        </div>
      </div>
    </div>
  </main>
</template>
