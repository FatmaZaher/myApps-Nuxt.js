<template>
  <div>
    <div class="section-1">
      <div class="section-img mx-auto">
        <img src="~/assets/images/animate-1.png" alt="img" class="img-back" />
        <img src="~/assets/images/animate-2.png" alt="img" class="img-front" />
      </div>
    </div>
    <b-container>
      <div class="section-2">
        <b-row>
          <b-col md="6" class="d-flex align-items-center">
            <div>
              <h3 class="mb-4">رؤيتنا</h3>
              <p>
                تطبيقاتي هو دليلك لأهم التـطبيقات الـموثوقـة التي تحتاجها بشكل
                دائم والتي تخص الجهات الحكوميـة والـشـركـات الخـدمــية فـي كــل
                الاهتمــامــات مثـل الخدمـات الحكومـية وخدمات التسـوق
                والاتصـالات والتطبيقات التعليميةوالإعلامية وتطبيقات المطاعم
                والصيـانة والتطبيقـات الصحيـة وكـذلك التطبيقـات الخاصـة بالبنـوك
                والمدفوعـات المـالـية
              </p>
            </div>
          </b-col>
          <b-col md="6" class="d-flex justify-content-center">
            <Mission />
          </b-col>
        </b-row>
      </div>
      <div class="section-3 py-5">
        <h3 class="mb-5">أقسام المواقع</h3>
        <b-row>
          <b-col
            v-for="service in services"
            :key="service.ServiceTypeId"
            class="serviceCard mb-5"
            md="4"
            lg="3"
          >
            <nuxt-link
              class="card-link"
              :to="'/service/' + service.ServiceTypeId"
            >
              <b-card
                :title="service.ServiceTypeName"
                :img-src="service.ImageURL"
                img-alt="Image"
                img-top
                tag="article"
              >
              </b-card>
            </nuxt-link>
          </b-col>
        </b-row>
      </div>
    </b-container>
  </div>
</template>
<script>
export default {
  data() {
    return {}
  },
  async asyncData({ $axios, error }) {
    try {
      const { data } = await $axios.get(
        'https://myapps.cc/wcf/service.svc/getServicesTypeList'
      )
      return {
        services: data,
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
