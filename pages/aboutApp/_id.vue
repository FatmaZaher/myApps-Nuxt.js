<template>
  <div v-if="infoApp" class="paddingPage about">
    <b-container>
      <h1 class="mb-5">{{pagetilte.ServiceName}}</h1>
      <b-card
        :img-src="infoApp.ServiceURL"
        img-alt="Image"
        img-top
        tag="article"
      >
        <div class="down-link mt-4 mb-5">
          <a href="#">
            <img src="~/assets/images/google-play.png" alt="google-play" />
            <span>تحميل التطبيق</span>
          </a>
          <a href="#">
            <i class="fab fa-apple"></i>
            <span>تحميل التطبيق</span>
          </a>
        </div>
        <b-card-text class="my-4" v-html="infoApp.ServiceDescription">
        </b-card-text>
      </b-card>
    </b-container>
  </div>
</template>
<script>
export default {
  async asyncData({ $axios, params, error }) {
    try {
      const { data } = await $axios.get(
        'https://myapps.cc/wcf/service.svc/getServiceById/' + params.id
      )
      const parent = data.ParentId
      const infoApp = data
      const paretnData = await $axios.get(
        'https://myapps.cc/wcf/service.svc/getServiceChildById/' +
          parent
      )
      const pagetilte = paretnData.data.find(
        (item) => item.ServiceId == params.id
      )
      return {
        infoApp,
        pagetilte,
      }
    } catch (e) {
      error({
        statusCode: 503,
        message: 'Unable to fetch evens at this time, Please try again.',
      })
    }
  },
}
</script>
<style scoped lang="scss">
</style>
