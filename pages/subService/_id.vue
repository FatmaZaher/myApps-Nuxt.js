<template>
  <div class="paddingPage">
    <b-container>
      <h2 class="mb-5" v-if="pagetilte">
        {{ pagetilte.ServiceName }}
      </h2>
      <b-row>
        <b-col
          v-for="(service, index) in subservices"
          :key="index"
          md="4"
          lg="3"
          class="serviceCard mb-5"
        >
          <nuxt-link class="card-link" :to="'/'">
            <b-card
              :title="service.ServiceName"
              :img-src="service.ServiceURL"
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
      const { data } = await $axios.get(
        'https://myapps.cc/wcf/service.svc/getServiceChildById/' + params.id
      )
      const parent = data[0].ServiceTypeId
      const subservices = data
      const paretnData = await $axios.get(
        'https://myapps.cc/wcf/service.svc/getServicesListByServiceTypeId/' +
          parent
      )
      const pagetilte = paretnData.data.find(
        (item) => item.ServiceId == params.id
      )
      return {
        subservices,
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
<style scoped></style>
