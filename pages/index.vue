<template>
  <v-container>
    <v-row justify="center" align="center">
      <v-col cols="12" sm="8" md="6">
        <div class="text-center">
          <logo />
          <vuetify-logo />
        </div>
        <v-card>
          <v-card-title class="headline">
            {{ $t('index.welcomeCard.title') }}
            {{ require('../package.json').appName }}
          </v-card-title>
          <v-card-text>
            <p v-html="$t('index.welcomeCard.text.p1')"></p>
            <p v-html="$t('index.welcomeCard.text.p2')"></p>
            <!-- <p v-html="$t('index.welcomeCard.text.p3')"></p> -->
            <!-- <p v-html="$t('index.welcomeCard.text.p4')"></p> -->
            <!-- <p v-html="$t('index.welcomeCard.text.p5')"></p> -->
            <div class="text-xs-right">
              <em>
                <small>&mdash; {{ $t('index.welcomeCard.text.p6') }}</small>
              </em>
            </div>
            <!-- <hr class="my-3" /> -->
            <a
              href="https://nuxtjs.org/"
              target="_blank"
              rel="noopener noreferrer"
            >
              {{ $t('index.welcomeCard.text.nuxtDocumentation') }}
            </a>
            <br />
            <a
              href="https://github.com/nuxt/nuxt.js"
              target="_blank"
              rel="noopener noreferrer"
            >
              {{ $t('index.welcomeCard.text.nuxtGitHub') }}
            </a>
          </v-card-text>
          <v-card-actions>
            <v-spacer />
            <v-btn color="primary" nuxt to="/inspire">
              {{ $t('index.welcomeCard.action.continue') }}
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
    <v-row justify="center" align="center">
      <v-col cols="12" sm="8" md="6">
        <v-card>
          <v-card-title class="headline">
            {{ $t('index.customLoadingCard.title') }}
          </v-card-title>
          <v-card-text>
            <p v-html="$t('index.customLoadingCard.text.p1')"></p>
            <a
              href="https://nuxtjs.org/docs/2.x/configuration-glossary/configuration-loading/#using-a-custom-loading-component"
              target="_blank"
              rel="noopener noreferrer"
            >
              {{ $t('index.customLoadingCard.text.nuxtDocumentation') }}
            </a>
            <br />
            <a
              href="https://v2.vuetifyjs.com/en/components/progress-circular/"
              target="_blank"
              rel="noopener noreferrer"
            >
              {{ $t('index.customLoadingCard.text.vuetifyDocumentation') }}
            </a>
          </v-card-text>
          <v-card-actions>
            <v-spacer />
            <v-btn color="primary" @click="loadingWithoutProgress()">
              {{ $t('index.customLoadingCard.action.withoutProgress') }}
            </v-btn>
            <v-btn color="primary" @click="loadingWithProgress()">
              {{ $t('index.customLoadingCard.action.withProgress') }}
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
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
export default class Index extends Vue {
  interval = {}

  async loadingWithoutProgress() {
    this.$nuxt.$loading.start()
    await this.sleep(5000)
    this.$nuxt.$loading.finish()
  }

  async loadingWithProgress() {
    this.$nuxt.$loading.start()
    this.$nuxt.$loading.increase!(0)
    const max = 10
    for (let i = 0; i < max; i++) {
      await this.sleep(500)
      this.updateLoadingProgress(i, max)
    }
    await this.sleep(1000)
    this.$nuxt.$loading.finish()
  }

  updateLoadingProgress(currentIndex: number, total: number) {
    this.$nuxt.$loading.increase!(
      Math.round(((currentIndex + 1) / total) * 100)
    )
  }

  sleep(msec: number) {
    return new Promise((resolve) => setTimeout(resolve, msec))
  }

  head() {
    return {
      // Page title is "appName"
      titleTemplate: '',
      title: require('../package.json').appName,
    }
  }
}
</script>
