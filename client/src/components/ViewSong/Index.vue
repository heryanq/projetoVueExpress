<template>
  <div>
    <v-container padding fluid>
      <v-layout>
        <v-flex xs4>
          <song-metadata :song="song" />
        </v-flex>
    
        <v-flex xs4 class="ml-2">
          <lyrics :song="song" />
        </v-flex>

        <v-flex xs4 class="ml-2">
          <you-tube :youtubeId="song.youtubeId" />
        </v-flex>
      </v-layout>
    </v-container>
  </div>
</template>

<script>
import {mapState} from 'vuex'
import Lyrics from './Lyrics'
import SongMetadata from './SongMetadata'
import YouTube from './YouTube'
import SongsService from '@/services/SongsService'
import SongHistoryService from '@/services/SongHistoryService'

export default {
  data () {
    return {
      song: {}
    }
  },
  computed: {
    ...mapState([
      'isUserLoggedIn',
      'user',
      'route'
    ])
  },
  async mounted () {
    const songId = this.route.params.songId
    this.song = (await SongsService.show(songId)).data

    if (this.isUserLoggedIn) {
      SongHistoryService.post({
        songId: songId
      })
    }
  },
  components: {
    SongMetadata,
    YouTube,
    Lyrics
  }
}
</script>

<style scoped>

.container.fluid {
  max-width: 80%;
}

.padding {
  padding-top: 50px;
  padding-right: 50px;
  padding-bottom: 10px;
  padding-left: 50px;
}

</style>
