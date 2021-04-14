<template>
  <v-app>
    <v-navigation-drawer
      v-model="drawer"
      :mini-variant="miniVariant"
      :clipped="clipped"
      fixed
      app
    >
      <v-list>
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          router
          :exact="item.exact"
          color="primary"
        >
          <v-tooltip right>
            <template v-slot:activator="{ on, attrs }">
              <v-list-item-action v-bind="attrs" v-on="on">
                <v-icon>{{ item.icon }}</v-icon>
              </v-list-item-action>
            </template>
            <span>{{ item.title }}</span>
          </v-tooltip>
          <v-list-item-content>
            <v-list-item-title v-text="item.title" />
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar :clipped-left="clipped" fixed app dark color="primary">
      <v-app-bar-nav-icon
        @click.stop="
          if (drawer) {
            drawer = !miniVariant ? !miniVariant : miniVariant
            miniVariant = !miniVariant
          } else {
            drawer = !drawer
            miniVariant = false
          }
        "
      />
      <v-toolbar-title v-text="$t('appName')" />
      <v-spacer />
      <v-tooltip bottom>
        <template v-slot:activator="{ on, attrs }">
          <v-btn
            icon
            :to="switchLocalePath(getNextLanguage())"
            v-bind="attrs"
            v-on="on"
          >
            <v-icon>mdi-translate</v-icon>
          </v-btn>
        </template>
        <span>{{ $t('switchLanguage') }}</span>
      </v-tooltip>
      <v-tooltip bottom>
        <template v-slot:activator="{ on, attrs }">
          <v-btn icon v-bind="attrs" v-on="on" @click="invertColors">
            <v-icon>mdi-invert-colors</v-icon>
          </v-btn>
        </template>
        <span>{{ $t('switchTheme') }}</span>
      </v-tooltip>
    </v-app-bar>
    <v-main>
      <v-container>
        <nuxt />
      </v-container>
    </v-main>
    <v-footer :absolute="!fixed" inset app>
      <span>&copy; {{ new Date().getFullYear() }} {{ author }}</span>
      <v-spacer />
      <span>v{{ version }}</span>
    </v-footer>
  </v-app>
</template>

<script lang="ts">
import { Vue, Component } from 'nuxt-property-decorator'

@Component
export default class DefaultLayout extends Vue {
  declare localePath: any
  declare $i18n: any

  title = require('../package.json').appName
  version = require('../package.json').version
  author = require('../package.json').author
  dark = this.isDark()
  lang = ''
  nextLang = ''
  clipped = true
  drawer = null
  fixed = false
  miniVariant = true
  items = [
    {
      icon: 'mdi-apps',
      title: (this as any).$t('menu.index'),
      to: (this as any).localePath('index', (this as any).$i18n.locale),
      exact: true, // If root page, it should be "true".
    },
    {
      icon: 'mdi-chart-bubble',
      title: (this as any).$t('menu.inspire'),
      to: (this as any).localePath('inspire', (this as any).$i18n.locale),
      exact: false, // If the page has child pages (e.g. /inspire/edit), it should be "false".
    },
  ]

  mounted() {
    // Set default theme
    this.$vuetify.theme.dark = this.isDark()

    // Set default language
    this.lang = this.getLanguage()
    if (this.lang !== this.$i18n.locale) {
      this.$router.push(this.localePath('index', this.lang))
    }
  }

  updated() {
    // Update language setting
    if (this.lang !== this.$i18n.locale) {
      this.lang = this.$i18n.locale
      localStorage.setItem('lang', this.lang)
      // Update link of navigation drawer
      this.items.forEach((item, i) => {
        const path = item.to.split('/')
        const routeName =
          path[path.length - 1] !== ''
            ? path[path.length - 1] !== this.getNextLanguage()
              ? path[path.length - 1]
              : 'index'
            : 'index'
        if (this.$i18n.locale === this.$i18n.defaultLocale) {
          this.items[i].title = (this as any).$t(`menu.${routeName}`)
          this.items[i].to =
            path[path.length - 1] !== this.getNextLanguage()
              ? '/' + path[path.length - 1]
              : '/'
        } else {
          this.items[i].title = (this as any).$t(`menu.${routeName}`)
          this.items[i].to =
            '/' + this.$i18n.locale + '/' + path[path.length - 1]
        }
      })
    }
  }

  invertColors() {
    this.dark = !this.dark
    this.$vuetify.theme.dark = this.dark
    localStorage.setItem('dark', this.dark.toString())
  }

  isDark(): boolean {
    return localStorage.getItem('dark') !== null
      ? localStorage.getItem('dark') === 'true'
      : true
  }

  getLanguage(): string {
    const language = localStorage.getItem('lang')
    return language !== null ? language : 'en'
  }

  getNextLanguage(): string {
    if (this.lang === '' || this.lang === 'en') {
      return 'ja'
    } else {
      return 'en'
    }
  }

  head(): object {
    return {
      // Page title is "title - appName"
      titleTemplate: '%s - ' + (this as any).$t('appName'),
    }
  }
}
</script>
