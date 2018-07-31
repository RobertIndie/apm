<template>
  <div class="animated fadeIn">
    <b-card header-tag="header">
      <div slot="header">
        <i class="icon-calendar"></i> 今日到期
      </div>
      <b-card-body>
        <b-row v-if="true">
            <b-col v-for="item in otherTodoTask" :key="item._id">
              <task :taskObj="item"></task>
            </b-col>
        </b-row>
        <b-row v-else>
          <b-col>无</b-col>
        </b-row>
      </b-card-body>
    </b-card>
    <b-card header-tag="header">
      <div slot="header">
        <i class="icon-calendar"></i> 其他
      </div>
      <b-card-body>
        <b-row>

        </b-row>
      </b-card-body>
    </b-card>
  </div>
</template>

<script>
import Task from './Task'

export default {
  name: 'todolist',
  components: {  
    Task
  },
  data: function () {
    return {
      todayTodoTask:[

      ],
      otherTodoTask:[
        {
          _id: 1000,
          name: '测试任务',
          description: '任务简介'
        }
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
  },
  methods: {
    select () {
      alert("select");
    }
  }
}
</script>
