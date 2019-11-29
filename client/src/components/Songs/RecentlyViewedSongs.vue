<template>
  <div>
    <v-container fluid padding>
      <panel title="Recently Viewed Songs">
        <v-data-table
          :headers="headers"
          :pagination.sync="pagination"
          :items="histories">
          <template slot="items" scope="props">
            <td class="text-xs-right">
              {{props.item.title}}
            </td>
            <td class="text-xs-right">
              {{props.item.artist}}
            </td>
          </template>
        </v-data-table>
      </panel>
    </v-container>
  </div>
</template>

<script>
import {mapState} from 'vuex'
import SongHistoryService from '@/services/SongHistoryService'

export default {
  data () {
    return {
      headers: [
        {
          text: 'Title',
          value: 'title'
        },
        {
          text: 'Artist',
          value: 'artist'
        }
      ],
      pagination: {
        sortBy: 'createdAt',
        descending: true
      },
      histories: []
    }
  },
  computed: {
    ...mapState([
      'isUserLoggedIn',
      'user'
    ])
  },
  async mounted () {
    if (this.isUserLoggedIn) {
      this.histories = (await SongHistoryService.index()).data
    }
  }
}
</script>

<style>

.padding {
  padding-left: 100px;
}

</style>
