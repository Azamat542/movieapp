<template>
  <div class="p-8">
    <div class="movie-info border-b border-gray-800">
      <div class="container mx-auto px-4 py-16 flex flex-col md:flex-row">
        <div class="flex-none">
          <img
            v-if="actor.profile_path"
            :src="`https://image.tmdb.org/t/p/w300${actor.profile_path}`"
            alt="profile image"
            class="w-76"
          />
          <ul class="flex items-center mt-4">
            <li v-if="socialLinks && actor.external_ids.facebook_id">
              <a
                :href="`https://facebook.com/${actor.external_ids.facebook_id}`"
                title="Facebook"
                target="_blank"
              >
                <svg class="fill-current text-gray-400 hover:text-white w-6" viewBox="0 0 448 512">
                  <path
                    d="M448 56.7v398.5c0 13.7-11.1 24.7-24.7 24.7H309.1V306.5h58.2l8.7-67.6h-67v-43.2c0-19.6 5.4-32.9 33.5-32.9h35.8v-60.5c-6.2-.8-27.4-2.7-52.2-2.7-51.6 0-87 31.5-87 89.4v49.9h-58.4v67.6h58.4V480H24.7C11.1 480 0 468.9 0 455.3V56.7C0 43.1 11.1 32 24.7 32h398.5c13.7 0 24.8 11.1 24.8 24.7z"
                  />
                </svg>
              </a>
            </li>

            <li class="ml-6" v-if="socialLinks && actor.external_ids.instagram_id">
              <a
                :href="`https://instagram.com/${actor.external_ids.instagram_id}`"
                title="Instagram Handle"
                target="_blank"
              >
                <svg class="fill-current text-gray-400 hover:text-white w-6" viewBox="0 0 448 512">
                  <path
                    d="M224.1 141c-63.6 0-114.9 51.3-114.9 114.9s51.3 114.9 114.9 114.9S339 319.5 339 255.9 287.7 141 224.1 141zm0 189.6c-41.1 0-74.7-33.5-74.7-74.7s33.5-74.7 74.7-74.7 74.7 33.5 74.7 74.7-33.6 74.7-74.7 74.7zm146.4-194.3c0 14.9-12 26.8-26.8 26.8-14.9 0-26.8-12-26.8-26.8s12-26.8 26.8-26.8 26.8 12 26.8 26.8zm76.1 27.2c-1.7-35.9-9.9-67.7-36.2-93.9-26.2-26.2-58-34.4-93.9-36.2-37-2.1-147.9-2.1-184.9 0-35.8 1.7-67.6 9.9-93.9 36.1s-34.4 58-36.2 93.9c-2.1 37-2.1 147.9 0 184.9 1.7 35.9 9.9 67.7 36.2 93.9s58 34.4 93.9 36.2c37 2.1 147.9 2.1 184.9 0 35.9-1.7 67.7-9.9 93.9-36.2 26.2-26.2 34.4-58 36.2-93.9 2.1-37 2.1-147.8 0-184.8zM398.8 388c-7.8 19.6-22.9 34.7-42.6 42.6-29.5 11.7-99.5 9-132.1 9s-102.7 2.6-132.1-9c-19.6-7.8-34.7-22.9-42.6-42.6-11.7-29.5-9-99.5-9-132.1s-2.6-102.7 9-132.1c7.8-19.6 22.9-34.7 42.6-42.6 29.5-11.7 99.5-9 132.1-9s102.7-2.6 132.1 9c19.6 7.8 34.7 22.9 42.6 42.6 11.7 29.5 9 99.5 9 132.1s2.7 102.7-9 132.1z"
                  />
                </svg>
              </a>
            </li>

            <li class="ml-6" v-if="actor.homepage">
              <a :href="actor.homepage" title="Website" target="_blank">
                <svg class="fill-current text-gray-400 hover:text-white w-6" viewBox="0 0 496 512">
                  <path
                    d="M248 8C111.03 8 0 119.03 0 256s111.03 248 248 248 248-111.03 248-248S384.97 8 248 8zm82.29 357.6c-3.9 3.88-7.99 7.95-11.31 11.28-2.99 3-5.1 6.7-6.17 10.71-1.51 5.66-2.73 11.38-4.77 16.87l-17.39 46.85c-13.76 3-28 4.69-42.65 4.69v-27.38c1.69-12.62-7.64-36.26-22.63-51.25-6-6-9.37-14.14-9.37-22.63v-32.01c0-11.64-6.27-22.34-16.46-27.97-14.37-7.95-34.81-19.06-48.81-26.11-11.48-5.78-22.1-13.14-31.65-21.75l-.8-.72a114.792 114.792 0 01-18.06-20.74c-9.38-13.77-24.66-36.42-34.59-51.14 20.47-45.5 57.36-82.04 103.2-101.89l24.01 12.01C203.48 89.74 216 82.01 216 70.11v-11.3c7.99-1.29 16.12-2.11 24.39-2.42l28.3 28.3c6.25 6.25 6.25 16.38 0 22.63L264 112l-10.34 10.34c-3.12 3.12-3.12 8.19 0 11.31l4.69 4.69c3.12 3.12 3.12 8.19 0 11.31l-8 8a8.008 8.008 0 01-5.66 2.34h-8.99c-2.08 0-4.08.81-5.58 2.27l-9.92 9.65a8.008 8.008 0 00-1.58 9.31l15.59 31.19c2.66 5.32-1.21 11.58-7.15 11.58h-5.64c-1.93 0-3.79-.7-5.24-1.96l-9.28-8.06a16.017 16.017 0 00-15.55-3.1l-31.17 10.39a11.95 11.95 0 00-8.17 11.34c0 4.53 2.56 8.66 6.61 10.69l11.08 5.54c9.41 4.71 19.79 7.16 30.31 7.16s22.59 27.29 32 32h66.75c8.49 0 16.62 3.37 22.63 9.37l13.69 13.69a30.503 30.503 0 018.93 21.57 46.536 46.536 0 01-13.72 32.98zM417 274.25c-5.79-1.45-10.84-5-14.15-9.97l-17.98-26.97a23.97 23.97 0 010-26.62l19.59-29.38c2.32-3.47 5.5-6.29 9.24-8.15l12.98-6.49C440.2 193.59 448 223.87 448 256c0 8.67-.74 17.16-1.82 25.54L417 274.25z"
                  />
                </svg>
              </a>
            </li>
          </ul>
        </div>
        <div class="md:ml-24">
          <h2 class="text-4xl mt-4 md:mt-0 font-semibold">{{actor.name}}</h2>
          <div class="flex flex-wrap items-center text-gray-400 text-sm">
            <svg class="fill-current text-gray-400 hover:text-white w-4" viewBox="0 0 448 512">
              <path
                d="M448 384c-28.02 0-31.26-32-74.5-32-43.43 0-46.825 32-74.75 32-27.695 0-31.454-32-74.75-32-42.842 0-47.218 32-74.5 32-28.148 0-31.202-32-74.75-32-43.547 0-46.653 32-74.75 32v-80c0-26.5 21.5-48 48-48h16V112h64v144h64V112h64v144h64V112h64v144h16c26.5 0 48 21.5 48 48v80zm0 128H0v-96c43.356 0 46.767-32 74.75-32 27.951 0 31.253 32 74.75 32 42.843 0 47.217-32 74.5-32 28.148 0 31.201 32 74.75 32 43.357 0 46.767-32 74.75-32 27.488 0 31.252 32 74.5 32v96zM96 96c-17.75 0-32-14.25-32-32 0-31 32-23 32-64 12 0 32 29.5 32 56s-14.25 40-32 40zm128 0c-17.75 0-32-14.25-32-32 0-31 32-23 32-64 12 0 32 29.5 32 56s-14.25 40-32 40zm128 0c-17.75 0-32-14.25-32-32 0-31 32-23 32-64 12 0 32 29.5 32 56s-14.25 40-32 40z"
              />
            </svg>
            <span
              class="ml-2"
            >{{ actor.birthday | formatDate}} ({{ actor.birthday | age}} years old) in {{actor.place_of_birth }}</span>
          </div>

          <p class="text-gray-300 mt-8">{{actor.biography}}</p>

          <h4 class="font-semibold mt-12">Known For</h4>

          <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-5 gap-8">
            <div class="mt-4" v-for="movie in credits.slice(0,5)" :key="movie.credit_id">
              <router-link :to="{ name: movie.media_type == 'person' ? 'ActorDetail' : (movie.media_type == 'tv' ? 'TvshowDetail' : 'MovieDetail'), params: { id: movie.id }}">
                <img
                  :src="`https://image.tmdb.org/t/p/w400${movie.poster_path}`"
                  alt="poster"
                  class="hover:opacity-75 transition ease-in-out duration-150"
                />
              </router-link>
              <router-link
                :to="{ name: movie.media_type == 'person' ? 'ActorDetail' : (movie.media_type == 'tv' ? 'TvshowDetail' : 'MovieDetail'), params: { id: movie.id }}"
                class="text-sm leading-normal block text-gray-400 hover:text-white mt-1"
              >{{movie.title ? movie.title : movie.name}}</router-link>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- end movie-info -->

    <div class="credits border-b border-gray-800">
      <div class="container mx-auto px-4 py-16">
        <h2 class="text-4xl font-semibold">Credits</h2>
        <ul class="list-disc leading-loose pl-5 mt-8">
          <li v-for="credit in credits" :key="credit.credit_id">
            {{credit.release_date ? credit.release_date : credit.first_air_date | yearFormat}} &middot;
            <strong>
              <router-link
                :to="{ name: credit.media_type == 'person' ? 'ActorDetail' : (credit.media_type == 'tv' ? 'TvshowDetail' : 'MovieDetail'), params: { id: credit.id }}"
                class="hover:underline"
              >{{credit.title ? credit.title : credit.name}}</router-link>
            </strong>
            <span v-if="credit.character">&nbsp; as {{credit.character}}</span>
          </li>
        </ul>
      </div>
    </div>
    <!-- end credits-->
  </div>
</template>

<script>
import { mapGetters } from "vuex";
export default {
  created() {
    this.$store.dispatch("actor/getActorDetail", this.$route.params.id);
  },
  computed: {
    ...mapGetters("actor", ["actor"]),
    credits() {
      const credits = Object.keys(this.actor).includes("combined_credits")
        ? this.actor.combined_credits.cast
        : [];
      return credits.sort((a, b) => {
        return b.vote_count - a.vote_count;
      });
    },
    socialLinks() {
      return Object.keys(this.actor).includes("external_ids");
    }
  }
};
</script>