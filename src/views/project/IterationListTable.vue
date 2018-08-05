<template>
  <b-card :header="caption">
    <b-table :hover="hover" :striped="striped" :bordered="bordered" :small="small" :fixed="fixed" responsive="sm" :items="items" :fields="fields" :current-page="currentPage" :per-page="perPage">
      <!-- <template slot="status" slot-scope="data">
        <b-badge :variant="getBadge(data.item.status)">{{data.item.status}}</b-badge>
      </template> -->
    </b-table>
    <nav>
      <b-pagination :total-rows="getRowCount(items)" :per-page="perPage" v-model="currentPage" prev-text="上一页" next-text="下一页" hide-goto-end-buttons/>
    </nav>
  </b-card>
</template>

<script>
/**
   * Randomize array element order in-place.
   * Using Durstenfeld shuffle algorithm.
   */
const shuffleArray = (array) => {
  for (let i = array.length - 1; i > 0; i--) {
    let j = Math.floor(Math.random() * (i + 1))
    let temp = array[i]
    array[i] = array[j]
    array[j] = temp
  }
  return array
}

export default {
  name: 'iterationListTable',
  props: {
    caption: {
      type: String,
      default: 'Table'
    },
    hover: {
      type: Boolean,
      default: false
    },
    striped: {
      type: Boolean,
      default: false
    },
    bordered: {
      type: Boolean,
      default: false
    },
    small: {
      type: Boolean,
      default: false
    },
    fixed: {
      type: Boolean,
      default: false
    }
  },
  data: () => {
    return {
      //name startDate endDate status
      items: shuffleArray([
        {'任务': 'Samppa Nori', '完成时间': '2012/01/01', '迭代': 'Member', status: 'Active'},
        {'任务': 'Estavan Lykos', '完成时间': '2012/02/01', '迭代': 'Staff', status: 'Banned'},
        {'任务': 'Chetan Mohamed', '完成时间': '2012/02/01', '迭代': 'Admin', status: 'Inactive'},
        {'任务': 'Derick Maximinus', '完成时间': '2012/03/01', '迭代': 'Member', status: 'Pending'},
        {'任务': 'Friderik Dávid', '完成时间': '2012/01/21', '迭代': 'Staff', status: 'Active'},
        {'任务': 'Yiorgos Avraamu', '完成时间': '2012/01/01', '迭代': 'Member', status: 'Active'},
        {'任务': 'Avram Tarasios', '完成时间': '2012/02/01', '迭代': 'Staff', status: 'Banned'},
        {'任务': 'Quintin Ed', '完成时间': '2012/02/01', '迭代': 'Admin', status: 'Inactive'},
        {'任务': 'Enéas Kwadwo', '完成时间': '2012/03/01', '迭代': 'Member', status: 'Pending'},
        {'任务': 'Agapetus Tadeáš', '完成时间': '2012/01/21', '迭代': 'Staff', status: 'Active'},
        {'任务': 'Carwyn Fachtna', '完成时间': '2012/01/01', '迭代': 'Member', status: 'Active'},
        {'任务': 'Nehemiah Tatius', '完成时间': '2012/02/01', '迭代': 'Staff', status: 'Banned'},
        {'任务': 'Ebbe Gemariah', '完成时间': '2012/02/01', '迭代': 'Admin', status: 'Inactive'},
        {'任务': 'Eustorgios Amulius', '完成时间': '2012/03/01', '迭代': 'Member', status: 'Pending'},
        {'任务': 'Leopold Gáspár', '完成时间': '2012/01/21', '迭代': 'Staff', status: 'Active'},
        {'任务': 'Pompeius René', '完成时间': '2012/01/01', '迭代': 'Member', status: 'Active'},
        {'任务': 'Paĉjo Jadon', '完成时间': '2012/02/01', '迭代': 'Staff', status: 'Banned'},
        {'任务': 'Micheal Mercurius', '完成时间': '2012/02/01', '迭代': 'Admin', status: 'Inactive'},
        {'任务': 'Ganesha Dubhghall', '完成时间': '2012/03/01', '迭代': 'Member', status: 'Pending'},
        {'任务': 'Hiroto Šimun', '完成时间': '2012/01/21', '迭代': 'Staff', status: 'Active'},
        {'任务': 'Vishnu Serghei', '完成时间': '2012/01/01', '迭代': 'Member', status: 'Active'},
        {'任务': 'Zbyněk Phoibos', '完成时间': '2012/02/01', '迭代': 'Staff', status: 'Banned'},
        {'任务': 'Einar Randall', '完成时间': '2012/02/01', '迭代': 'Admin', status: 'Inactive'},
        {'任务': 'Félix Troels', '完成时间': '2012/03/21', '迭代': 'Staff', status: 'Active'},
        {'任务': 'Aulus Agmundr', '完成时间': '2012/01/01', '迭代': 'Member', status: 'Pending'}
      ]),
      fields: [
        {key: '任务'},
        {key: '优先级'},
        {key: '截止时间'},
        {key: '状态'}
      ],
      currentPage: 1,
      perPage: 20,
      totalRows: 0
    }
  },
  methods: {
    getBadge (status) {
      return status === 'Active' ? 'success'
        : status === 'Inactive' ? 'secondary'
          : status === 'Pending' ? 'warning'
            : status === 'Banned' ? 'danger' : 'primary'
    },
    getRowCount (items) {
      return items.length
    }
  }
}
</script>
