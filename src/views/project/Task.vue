<template>
  <b-card >
    <div slot="header">
      {{taskObj.name}}
      <b-badge pill :variant="statusIcon" class="float-right">{{status}}</b-badge>
    </div>
    <b-row>
      <b-col>
        <b-card>
          {{taskObj.description}}
        </b-card>
      </b-col>
    </b-row>
    <b-form>
    <b-form-group
      label="截止时间"
      label-cols="4"
      :horizontal="true">
      <b-form-input plaintext type="text" :value="taskObj.deadline"></b-form-input>
    </b-form-group>
    <b-form-group
      label="优先级"
      label-cols="4"
      :horizontal="true">
      <b-form-input plaintext type="text" :value="priority"></b-form-input>
    </b-form-group>      
    <b-form-group
      label="状态"
      label-cols="4"
      :horizontal="true">
      <b-form-select id="status"
        :plain="true"
        @change="statusChanged"
        :options="['规划中','实现中','已实现','已放弃']"
        :value="status">
      </b-form-select>
    </b-form-group>         
    </b-form>
  </b-card>
</template>
    
<script>
export default {
  name: 'task',
  props: {
    taskObj: Object
  },
  data () {
    return {
      statusIcon: 'primary'
    }
  },
  computed: {
    status () {
      switch(this.taskObj.status){
        case 'planning' :{
          this.statusIcon='primary';
          return '规划中';
        }
        case 'developing':{
          this.statusIcon='info';
          return '实现中';
        }
        case 'resolved':{
          this.statusIcon='success';
          return '已实现';
        }
        case 'rejected':{
          this.statusIcon='danger';
          return '已放弃';
        }
      }
    },
    priority () {
      switch(this.taskObj.priority){
        case 'high':{
          return '高';
        }
        case 'middle':{
          return '中';
        }
        case 'low':{
          return '低';
        }
        case 'nice_to_have':{
          return '很低';
        }
      }
    }
  },
  methods: {
    statusChanged () {
      
    }
  }
}
</script>

<style>

</style>