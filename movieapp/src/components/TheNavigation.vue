<template>
  <header class="bg-gray-800 fixed w-full z-10 top-0">
    <div
      class="container mx-auto sm:flex sm:justify-between sm:items-center md:justify-start sm:px-4 sm:py-3"
    >
      <div class="flex items-center justify-between px-4 py-3 sm:p-0">
        <div>
          <router-link to="/">
            
          </router-link>
        </div>
        <p class="text-gray-200 uppercase font-semibold tracking-wide">
          <router-link to="/">Movieapp</router-link>
        </p>
        <span class="text-gray-100"></span>
        <div class="sm:hidden">
          <button
            @click="isOpen = !isOpen"
            type="button"
            class="block text-gray-500 hover:text-white focus:text-white focus:outline-none"
          >
           
          </button>
        </div>
      </div>
      <div
        class="container mx-auto px-4 flex flex-col md:flex-row items-center justify-between px-4 py-2"
      >
        <nav
          :class="isOpen ? 'block' : 'hidden'"
          class="px-2 pt-2 pb-4 sm:flex sm:p-0 text-sm ml-6"
        >
          <router-link
            to="/"
            class="block px-2 py-1 text-gray-400 hover:text-gray-100 font-medium rounded hover:bg-gray-800"
          >Movies</router-link>
          <router-link
            to="/tv-shows"
            class="mt-1 block px-2 py-1 text-gray-400 hover:text-gray-100 font-medium rounded hover:bg-gray-800 sm:mt-0 sm:ml-2"
          >TV</router-link>
          <router-link
            to="/actors"
            class="mt-1 block px-2 py-1 text-gray-400 hover:text-gray-100 font-medium rounded hover:bg-gray-800 sm:mt-0 sm:ml-2"
          >Actors</router-link>
        </nav>
        <div class="relative mt-3 md:mt-0">
          <input
            class="bg-gray-900 text-sm rounded-full w-64 px-4 pl-8 py-1 focus:outline-none focus:shadow-outline"
            placeholder="Search"
            v-model="keyword"
            @input="search"
            @keydown="isLoading = true"
          />
          <div class="absolute top-0">
            <svg class="fill-current w-4 text-gray-500 mt-2 ml-2" viewBox="0 0 24 24">
              <path
                class="heroicon-ui"
                d="M16.32 14.9l5.39 5.4a1 1 0 01-1.42 1.4l-5.38-5.38a8 8 0 111.41-1.41zM10 16a6 6 0 100-12 6 6 0 000 12z"
              />
            </svg>
          </div>

          <!-- <div class="spinner top-0 right-0 mr-4 mt-3"></div> -->
          <div class="absolute top-0 right-0 mt-3" v-if="isLoading">
            <div class="hollow-dots-spinner -mr-10">
              <div class="dot"></div>
              <div class="dot"></div>
              <div class="dot"></div>
            </div>
          </div>
          <div
            class="z-50 absolute bg-gray-700 text-sm rounded w-64 mt-4 search-list overflow-y-scroll"
            v-if="showSearchBox && sugestions.length"
          >
            <ul>
              <li v-for="(sugestion, i) in sugestions" :key="i" class="border-b border-gray-800">
                <router-link
                  :to="{ name: sugestion.media_type == 'person' ? 'ActorDetail' : (sugestion.media_type == 'tv' ? 'TvshowDetail' : 'MovieDetail'), params: { id: sugestion.id }}"
                >
                  <span
                    class="block hover:bg-gray-800 px-3 py-3 flex items-center transition ease-in-out duration-150 text-white"
                    @click="showSearchBox=false, keyword = ''"
                  >
                    <img
                      v-if="sugestion.poster_path"
                      :src="`https://image.tmdb.org/t/p/w92/${sugestion.poster_path}`"
                      alt="poster"
                      class="w-8"
                    />
                    <img v-else src="https://via.placeholder.com/50x75" alt="poster" class="w-8" />
                    <span
                      class="ml-4"
                    >{{ sugestion.name ? sugestion.name : sugestion.original_title }}</span>
                  </span>
                </router-link>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </header>
</template>

<script>
import _ from "lodash";
import axios from "axios";
export default {
  data() {
    return {
      isOpen: false,
      sugestions: "",
      keyword: "",
      showSearchBox: false,
      isLoading: false
    };
  },
  mounted() {
    document.body.addEventListener("keyup", e => {
      if (e.keyCode === 27) {
        this.showSearchBox = false;
      }
    });
  },
  methods: {
    search: _.debounce(function(e) {
      if (!e.target.value.length) {
        this.showSearchBox = false;
      } else {
        axios
          .get(
            "https://api.themoviedb.org/3/search/multi?query=" + e.target.value
          )
          .then(res => {
            this.showSearchBox = true;
            this.sugestions = res.data.results;
            this.isLoading = false
          });
      }
    }, 500)
  }
};
</script>

<style scoped>
::-webkit-scrollbar {
  width: 0px;
  background: transparent;
}
.search-list {
  height: 28rem;
}
.hollow-dots-spinner,
.hollow-dots-spinner * {
  box-sizing: border-box;
}

.hollow-dots-spinner {
  height: 15px;
  width: calc(30px * 3);
}

.hollow-dots-spinner .dot {
  width: 5px;
  height: 5px;
  margin: 0 calc(5px / 2);
  border: calc(5px / 5) solid gainsboro;
  border-radius: 50%;
  float: left;
  transform: scale(0);
  animation: hollow-dots-spinner-animation 1000ms ease infinite 0ms;
}

.hollow-dots-spinner .dot:nth-child(1) {
  animation-delay: calc(300ms * 1);
}

.hollow-dots-spinner .dot:nth-child(2) {
  animation-delay: calc(300ms * 2);
}

.hollow-dots-spinner .dot:nth-child(3) {
  animation-delay: calc(300ms * 3);
}

@keyframes hollow-dots-spinner-animation {
  50% {
    transform: scale(1);
    opacity: 1;
  }
  100% {
    opacity: 0;
  }
}
  a.router-link-exact-active{
    color: white;
  }
</style>