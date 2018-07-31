<template>
  <div class="animated fadeIn">
    <b-row>
      <b-col cols='12'>
        <b-card>
          <div slot="header">
            当前迭代
          </div>
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
        </b-card>
      </b-col>
    </b-row>
  </div>
</template>

<script>

export default {
  name: 'projectDashboard',
  components: {
    
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
