<template>
  <div class="animated fadeIn">
    <b-row>
      <b-col>
        <task-list-table  striped caption="<i class='fa fa-align-justify'></i> 当前迭代任务"></task-list-table>
      </b-col>
    </b-row>
  </div>
</template>

<script>
import TaskListTable from './TaskListTable'

export default {
  name: 'tasklist',
  components: {
    TaskListTable
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
