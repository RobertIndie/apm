<template>
  <div class="animated fadeIn">
    <b-card>
      <b-row>
        <b-col sm="5">
          <h4 id="traffic" class="card-title mb-0">贡献图</h4>
          <div class="small text-muted">{{now}}</div>
        </b-col>
        <!-- <b-col sm="7" class="d-none d-md-block">
          <b-button type="button" variant="primary" class="float-right"><i class="icon-cloud-download"></i></b-button>
          <b-button-toolbar class="float-right" aria-label="Toolbar with buttons group">
            <b-form-radio-group class="mr-3" id="radiosBtn" buttons button-variant="outline-secondary" v-model="selected" name="radiosBtn">
              <b-form-radio class="mx-0" value="Day">Day</b-form-radio>
              <b-form-radio class="mx-0" value="Month">Month</b-form-radio>
              <b-form-radio class="mx-0" value="Year">Year</b-form-radio>
            </b-form-radio-group>
          </b-button-toolbar>
        </b-col> -->
      </b-row>
      <main-chart-example chartId="main-chart-01" class="chart-wrapper" style="height:300px;margin-top:40px;" height="300"></main-chart-example>
    </b-card>
  </div>
</template>

<script>
import MainChartExample from './worktable/ContributeChart'

export default {
  name: 'worktable',
  components: {
    MainChartExample
  },
  mounted: function () {
    
  },
  data: function () {
    return {
      selected: 'Month'
    }
  },
  computed: {
    now: function () {
      return new Date().toLocaleDateString();
    } 
  },
  methods: {

  }
}
</script>

<style>

</style>
