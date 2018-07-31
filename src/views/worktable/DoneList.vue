<template>
  <div class="animated fadeIn">
    <b-low>
      <b-col>
        <done-list-table striped caption="<i class='fa fa-align-justify'></i> 已完成任务"></done-list-table>
      </b-col>
    </b-low>
  </div>
</template>

<script>
import DoneListTable from './DoneListTable';

export default {
  name: 'donelist',
  components: {
    DoneListTable
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
