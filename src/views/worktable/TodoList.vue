<template>
  <div class="animated fadeIn">
    <b-card header-tag="header">
      <div slot="header">
        <i class="icon-calendar"></i> 今日到期
      </div>
      <b-card-body>
        <b-row>
          <b-col v-for="item in todyTask" :key="item.id" sm="6" md="4">
              <b-card :header="item.name">
              {{item.name}}
              </b-card>
          </b-col>
        </b-row>
      </b-card-body>
    </b-card>
    <b-card header-tag="header">
      <div slot="header">
        <i class="icon-calendar"></i> 本次迭代
      </div>
      <b-card-body>
        <b-row>

        </b-row>
      </b-card-body>
    </b-card>
  </div>
</template>

<script>

export default {
  name: 'todolist',
  components: {  },
  data: function () {
    return {
      todyTask: [
        {
          id: 1,
          name: 'task1'
        },
        {
          id: 2,
          name: 'task2'
        }
      ]
    }
  }
}
</script>
