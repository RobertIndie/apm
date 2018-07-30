<template>
  <div class="animated fadeIn">
    <b-card header-tag="header">
      <div slot="header">
        <i class="icon-calendar"></i> 今日到期
      </div>
      <b-card-body>
        <b-row>
          <b-col v-for="item in otherTodoTask" :key="item._id" sm="6" md="4">
              <b-card :header="item.name">
              {{item.description}}
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
      todayTodoTask:[

      ],
      otherTodoTask:[

      ]
    }
  },
  mounted: function () {
    var todayDate = new Date().toLocaleDateString().replace(/\//g,'.');
    var todayTodoTasknextID = 0;
    var otherTodoTasknextID = 0;
    this.api.get(`/api/user/${this.GLOBAL.username}/todolist`).then(res => {
      res.data.forEach(element => {
        this.api.get(`/api/task/${element}`).then(res=>{
          var task = res.data;
          if(task.deadline===todayDate){
            task._id = todayTodoTasknextID;
            todayTodoTasknextID++;
            this.todayTodoTask.push(task);
          }
          else{
            task._id = otherTodoTasknextID;
            otherTodoTasknextID++;
            this.otherTodoTask.push(task);
          }
        });
      });
    });
  }
}
</script>
