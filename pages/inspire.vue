<template>
  <v-row>
    <v-col class="text-center">
      <img src="/v.png" alt="Vuetify.js" class="mb-5" />
      <blockquote class="blockquote">
        &#8220;{{ $t('inspire.message') }}&#8221;
        <footer>
          <small>
            <em>&mdash;{{ $t('inspire.from') }}</em>
          </small>
        </footer>
      </blockquote>
    </v-col>
  </v-row>
</template>

<script lang="ts">
import { Vue, Component } from 'nuxt-property-decorator'

@Component
export default class Inspire extends Vue {
  head() {
    return {
      // Page title is "title - appName"
      title: 'Inspire',
    }
  }
}
</script>
