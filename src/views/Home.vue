<template>
  <div class="ion-page">
    <ion-header>
      <ion-toolbar>
        <ion-title>PWA</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content class="ion-padding">
      <ZipSearch v-on:get-zip="getZipInfo" />
      <ClearInfo :info="info" v-on:clear-info="clearInfo" />
      <ZipInfo :info="info" />
    </ion-content>
  </div>
</template>

<script>
import ZipSearch from '../components/ZipSearch'
import ZipInfo from '../components/ZipInfo'
import ClearInfo from '../components/ClearInfo'

export default {
  name: 'home',
  components: { ZipSearch, ZipInfo, ClearInfo },
  data() {
    return {
      info: null,
    }
  },
  methods: {
    async getZipInfo(zip) {
      const res = await fetch(`https://api.zippopotam.us/us/${zip}`) 
      if (res.status == 404) {
        this.showAlert()
        return
      }
      this.info = await res.json()
    },
    showAlert() {
      return this.$ionic.alertController
        .create({
          header: "Enter Zipcode",
          message: "Please enter a valid US Zipcode",
          buttons: ["OK"] 
        })
        .then(a => a.present())
    },
    clearInfo() {
      this.info = null
    },
  },
}
</script>
