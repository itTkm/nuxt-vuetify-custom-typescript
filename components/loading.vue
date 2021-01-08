<template>
  <div
    v-if="loading"
    id="loading"
    :style="{
      '--background-color': getBackgroundColor(),
    }"
  >
    <v-progress-circular
      :color="getPrimaryColor()"
      :size="100"
      :width="10"
      :indeterminate="indeterminate"
      :rotate="rotate"
      :value="value"
    >
      <span v-if="!indeterminate">
        {{ value }}
      </span>
    </v-progress-circular>
  </div>
</template>

<script lang="ts">
import { Vue, Component } from 'nuxt-property-decorator'
import { VuetifyThemeItem } from 'vuetify/types/services/theme'

@Component
export default class CustomLoading extends Vue {
  loading = false
  indeterminate = true
  rotate = 0
  value = 0

  init() {
    this.indeterminate = true
    this.rotate = 0
    this.value = 0
  }

  start() {
    this.init()
    this.loading = true
  }

  finish() {
    this.loading = false
    this.init()
  }

  increase(value: number) {
    if (this.indeterminate) this.indeterminate = false
    this.rotate = -90
    this.value = value
  }

  getPrimaryColor(): VuetifyThemeItem {
    if (this.$vuetify.theme.dark) {
      return this.$vuetify.theme.themes.dark.primary
    } else {
      return this.$vuetify.theme.themes.light.primary
    }
  }

  getBackgroundColor() {
    if (this.$vuetify.theme.dark) {
      return this.hex2decColor('#000')
    } else {
      return this.hex2decColor('#fff')
    }
  }

  hex2decColor(hex: VuetifyThemeItem): string {
    const hexRgb = hex!.toString().replace('#', '')
    const hexR =
      hexRgb.length === 3
        ? hexRgb.substr(0, 1) + hexRgb.substr(0, 1)
        : hexRgb.substr(0, 2)
    const hexG =
      hexRgb.length === 3
        ? hexRgb.substr(1, 1) + hexRgb.substr(1, 1)
        : hexRgb.substr(2, 2)
    const hexB =
      hexRgb.length === 3
        ? hexRgb.substr(2, 1) + hexRgb.substr(2, 1)
        : hexRgb.substr(4, 2)
    return `${parseInt(hexR, 16)}, ${parseInt(hexG, 16)}, ${parseInt(hexB, 16)}`
  }
}
</script>

<style lang="scss">
#loading {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100vh;
  z-index: 9999;
  position: fixed;
  background-color: rgba(var(--background-color), 0.5);
  font-size: 25px;
}
</style>
