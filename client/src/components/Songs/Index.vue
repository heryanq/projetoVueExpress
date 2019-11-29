<template>
  <div>
    <v-container fluid>
      <v-layout>
        <v-flex xs4 v-if="isUserLoggedIn">
          <songs-bookmarks />
          <recently-viewed-songs class="mt-2" />
        </v-flex>

        <v-flex :class="{
            xs12: !isUserLoggedIn,
            xs8: isUserLoggedIn
          }" class="ml-2">
          <songs-search-panel />
          <songs-panel class="mt-2" />
        </v-flex>
      </v-layout>
    </v-container>
  </div>
</template>

<script>
import SongsPanel from './SongsPanel'
import SongsBookmarks from './SongsBookmarks'
import RecentlyViewedSongs from './RecentlyViewedSongs'
import SongsSearchPanel from './SongsSearchPanel'
import SongsService from '@/services/SongsService'
import {mapState} from 'vuex'

export default {
  components: {
    SongsPanel,
    SongsSearchPanel,
    SongsBookmarks,
    RecentlyViewedSongs
  },
  computed: {
    ...mapState([
      'isUserLoggedIn'
    ])
  },
  data () {
    return {
      songs: null
    }
  },
  async mounted () {
    this.songs = (await SongsService.index()).data
  }
}
</script>

<style scoped>
.song {
  padding: 20px;
  height: 330px;
  overflow: hidden;
}

.song-title {
  font-size: 30px;
}

.song-artist {
  font-size: 24px;
}

.song-genre {
  font-size: 18px;
}

.album-image {
  width: 70%;
  margin: 0 auto;
}

.container.fluid {
  max-width: 100%;
}

.padding {
  padding-top: 75px;
  padding-right: 0px;
  padding-bottom: 0px;
}

</style>
