<template>
  <div class="animated fadeIn">
    <b-row>
      <b-col cols='12'>
        <b-card>
          <div slot="header">
            当前迭代
          </div>
          <iteration-profile>
          </iteration-profile>
        </b-card>
      </b-col>
    </b-row>
  </div>
</template>

<script>
import IterationProfile from './IterationProfile';

export default {
  name: 'projectDashboard',
  components: {
    IterationProfile
  },
  data () {
    return {

    }
  },
  mounted () {

  },
  methods: {

  }
}
</script>

<style>

</style>
