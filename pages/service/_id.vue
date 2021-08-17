<template>
  <div class="paddingPage">
    <b-container>
      <h2 class="mb-5" v-if="serviceName">{{ serviceName.ServiceTypeName }}</h2>
      <b-row>
        <b-col
          v-for="(serviceItem, index) in serviceItems"
          :key="index"
          md="4"
          lg="3"
          class="serviceCard mb-5"
        >
          <nuxt-link class="card-link" :to="'/subService/' + serviceItem.ServiceId">
            <b-card
              :title="serviceItem.ServiceName"
              :img-src="serviceItem.ServiceURL"
              img-alt="Image"
              img-top
              tag="article"
            >
            </b-card>
          </nuxt-link>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>
<script>
export default {
  data() {
    return {}
  },
  async asyncData({ $axios, params, error }) {
    try {
      const serviceName = await $axios.get(
        'https://myapps.cc/wcf/service.svc/getServicesTypeList'
      )
      const serviceItems = await $axios.get(
        'https://myapps.cc/wcf/service.svc/getServicesListByServiceTypeId/' +
          params.id
      )
      return {
        serviceName: serviceName.data.find(
          (item) => item.ServiceTypeId == params.id
        ),
        serviceItems: serviceItems.data,
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
<style scoped lang="scss"></style>
