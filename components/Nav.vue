<template>
  <div class="nav">
    <b-container>
      <b-navbar>
        <b-navbar-brand>
          <nuxt-link :to="'/'"
            ><img src="~/assets/images/logo.png" alt="logo"
          /></nuxt-link>
        </b-navbar-brand>
        <b-navbar-nav>
          <b-nav-item>
            <nuxt-link :to="'/'">الرئيسية</nuxt-link>
          </b-nav-item>
          <b-nav-item>
            <nuxt-link :to="'/aboutApps'">عن تطبيقاتي</nuxt-link>
          </b-nav-item>
          <b-nav-form>
            <div class="search-box mx-3">
              <input
                class="search-input"
                type="text"
                name=""
                placeholder="إبحث عن تطبيقك هنا"
              />
              <a href="#" class="search-btn">
                <i class="fas fa-search"></i>
              </a>
            </div>
          </b-nav-form>
        </b-navbar-nav>
      </b-navbar>
    </b-container>
  </div>
</template>
<script>
export default {}
</script>
<style scoped></style>
