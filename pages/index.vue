<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <div class="text-center">
        <logo />
        <vuetify-logo />
      </div>
      <v-card>
        <v-card-title class="headline">
          {{ $t('index.cardTitle') }} {{ require('../package.json').appName }}
        </v-card-title>
        <v-card-text>
          <p v-html="$t('index.cardText.p1')"></p>
          <p v-html="$t('index.cardText.p2')"></p>
          <p v-html="$t('index.cardText.p3')"></p>
          <p v-html="$t('index.cardText.p4')"></p>
          <p v-html="$t('index.cardText.p5')"></p>
          <div class="text-xs-right">
            <em>
              <small>&mdash; {{ $t('index.cardText.p6') }}</small>
            </em>
          </div>
          <hr class="my-3" />
          <a
            href="https://nuxtjs.org/"
            target="_blank"
            rel="noopener noreferrer"
          >
            {{ $t('index.nuxtDocumentation') }}
          </a>
          <br />
          <a
            href="https://github.com/nuxt/nuxt.js"
            target="_blank"
            rel="noopener noreferrer"
          >
            {{ $t('index.nuxtGitHub') }}
          </a>
        </v-card-text>
        <v-card-actions>
          <v-spacer />
          <v-btn color="primary" nuxt to="/inspire">
            {{ $t('index.continue') }}
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-col>
  </v-row>
</template>

<script lang="ts">
import { Vue, Component } from 'nuxt-property-decorator'
import Logo from '~/components/Logo.vue'
import VuetifyLogo from '~/components/VuetifyLogo.vue'

@Component({
  components: {
    Logo,
    VuetifyLogo,
  },
})
export default class Index extends Vue {}
</script>
