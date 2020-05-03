<template>
  <div>
    <h1>Profile View</h1>
    <Loading v-if="isLoading" />
    <template v-if="profileData !== null">
      <MainBlock :profileData="profileData"/>
    </template>
  </div>
</template>

<script>
import setError from '@/mixins/setError'

import Loading from '@/components/Loading/Index'
import MainBlock from './MainBlock/Index'

import { getApiAccount } from '@/api/search'

export default {
  name: 'ProfileView',
  components: {
    Loading,
    MainBlock
  },
  mixins: [
    setError
  ],
  data: () => {
    return {
      isLoading: false,
      profileData: null
    }
  },
  created () {
    // this.$route.params -> { region: "eu", battleTag: "SuperRambo-2613" }
    this.fetchData()
  },
  methods: {
    fetchData () {
      const { region, battleTag: account } = this.$route.params
      // Llamada a la API con los datos necesarios          this.loading = true;
      this.loading = true
      getApiAccount({ region, account })
        .then(({ data }) => {
          this.loading = true
          this.profileData = data
        })
        .catch((err) => {
          this.profileData = null
          const errObj = {
            routeParams: this.$route.params,
            message: err.message
          }
          if (err.response) {
            errObj.data = err.response.data
            errObj.status = err.response.status
          }
          this.setApiErr(errObj)
          this.$router.push({ name: 'Error' })
        })
        .finally(() => {
          this.loading = false
        })
    }
  }
}
</script>
