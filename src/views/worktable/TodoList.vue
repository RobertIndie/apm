<template>
  <div class="animated fadeIn">
    <b-card header-tag="header">
      <div slot="header">
        <i class="icon-calendar"></i> 今日到期
      </div>
      <b-card-body>
        <b-row v-if="true">
            <b-col v-for="item in otherTodoTask" :key="item._id">
              <b-card >
                <div slot="header">
                  {{item.name}}
                  <b-badge pill variant="danger" class="float-right">Planning</b-badge>
                </div>
                <b-row>
                  <b-col>
                    <b-card>
                      {{item.description}}
                    </b-card>
                  </b-col>
                </b-row>
                <b-form>
                <b-form-group
                  label="截止时间"
                  label-cols="4"
                  :horizontal="true">
                  <b-form-input plaintext type="text" value="今天"></b-form-input>
                </b-form-group>
                <b-form-group
                  label="优先级"
                  label-cols="4"
                  :horizontal="true">
                  <b-form-input plaintext type="text" value="高破天际"></b-form-input>
                </b-form-group>      
                <b-form-group
                  label="状态"
                  label-cols="4"
                  :horizontal="true">
                  <b-form-select id="state"
                    :plain="true"
                    @change="select()"
                    :options="['规划中','实现中','已实现','已放弃']"
                    value="规划中">
                  </b-form-select>
                </b-form-group>         
                </b-form>
              </b-card>
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

export default {
  name: 'todolist',
  components: {  },
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
