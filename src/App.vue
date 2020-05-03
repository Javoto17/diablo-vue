<template>
  <div id="app">

    <LoadLayout v-if="isLoading">
      <Loading/>
    </LoadLayout>

    <MainLayout v-else/>

  </div>
</template>

<script>
import { mapState } from 'vuex'

import LoadLayout from './layouts/LoadLayout'
import MainLayout from './layouts/MainLayout'
import Loading from '@/components/Loading/Index'

export default {
  name: 'App',
  components: {
    MainLayout,
    LoadLayout,
    Loading
  },
  computed: {
    ...mapState('loading', {
      isLoading: 'isLoading'
    })
  }
}
</script>

<style lang="stylus">
#app
  font-family Avenir, Helvetica, Arial, sans-serif
  -webkit-font-smoothing antialiased
  -moz-osx-font-smoothing grayscale
  text-align left
  color #2c3e50
  margin-top 60px
  color: #e1cf9d
  background-color #12110f
html
  background-color #12110f
</style>
