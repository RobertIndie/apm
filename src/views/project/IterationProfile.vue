<template>
  <div>
    <b-form>
      <b-form-group
        label="迭代名称"
        label-cols="4"
        :horizontal="true">
        <b-form-input plaintext type="text" :value="currentIteration.name"></b-form-input>
      </b-form-group>
      <b-form-group
        label="迭代简介"
        label-cols="4"
        :horizontal="true">
        <p>
          {{currentIteration.description}}
        </p>
      </b-form-group>
      <b-form-group
        label="迭代开始时间"
        label-cols="4"
        :horizontal="true">
        <b-form-input plaintext type="text" :value="currentIteration.startDate"></b-form-input>
      </b-form-group>
      <b-form-group
        label="迭代截止时间"
        label-cols="4"
        :horizontal="true">
        <b-form-input plaintext type="text" :value="currentIteration.endDate"></b-form-input>
      </b-form-group>
      <b-form-group
        label="迭代进度"
        label-cols="4"
        :horizontal="true">
        <b-progress class="mt-1" :max="30" show-value>
          <b-progress-bar :value="resolved" variant="success"></b-progress-bar>
          <b-progress-bar :value="developing" variant="warning"></b-progress-bar>
          <b-progress-bar :value="rejected" variant="danger"></b-progress-bar>
        </b-progress>
      </b-form-group>
    </b-form>
    <b-row>
      <b-col>
        <b-card>
          <b-row>
            <b-col>
              <h4 class="text-center card-title">任务规模燃烧图</h4>
            </b-col>
          </b-row>
          <b-row>
            <b-col>
              <size-burn-chart></size-burn-chart>
            </b-col>
          </b-row>
        </b-card>
      </b-col>
    </b-row>
    <b-row>
      <b-col>
        <b-card>
          <b-row>
            <b-col>
              <h4 class="text-center card-title">任务个数燃烧图</h4>
            </b-col>
          </b-row>
          <b-row>
            <b-col>
              <count-burn-chart></count-burn-chart>
            </b-col>
          </b-row>
        </b-card>
      </b-col>
    </b-row>
    <b-row>
      <b-col md="6">
        <b-card>
          <b-row>
            <b-col>
              <h4 class="text-center card-title">任务状态分布图</h4>
            </b-col>
          </b-row>
          <b-row>
            <b-col>
              <status-distribute-chart></status-distribute-chart>
            </b-col>
          </b-row>
        </b-card>
      </b-col>
      <b-col md="6">
        <b-card>
          <b-row>
            <b-col>
              <h4 class="text-center card-title">任务规模分布图</h4>
            </b-col>
          </b-row>
          <b-row>
            <b-col>
              <size-distribute-chart></size-distribute-chart>
            </b-col>
          </b-row>
        </b-card>
      </b-col>
    </b-row>
  </div>
</template>

<script>
import SizeBurnChart from './charts/SizeBurnChart';
import CountBurnChart from './charts/CountBurnChart';
import StatusDistributeChart from './charts/StatusDistributeChart';
import SizeDistributeChart from './charts/SizeDistributeChart';

export default {
  name: 'iterationProfile',
  components: {
    SizeBurnChart,
    CountBurnChart,
    StatusDistributeChart,
    SizeDistributeChart
  },
  props: {
    iterationObj: Object
  },
  data () {
    return {
      project: {},
      currentIteration: {},
      resolved: 10,
      developing: 3,
      rejected: 1
    }
  },
  mounted () {
      this.api.get(`/api/project/${this.GLOBAL.projectID}`).then(res=>{
      this.project = res.data;
      this.api.get(`/api/iteration/${this.project.currentIteration}`).then(res=>{
        this.currentIteration = res.data;
      });
    });
  },
  methods: {

  }
}
</script>

<style>

</style>
