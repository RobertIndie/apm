<script>
import { Pie } from 'vue-chartjs'
import { getStyle, hexToRgba } from '@coreui/coreui/dist/js/coreui-utilities'

export default {
  name: 'sizeDistributeChart',
  extends: Pie,
  mounted () {
    this.renderChart({
      labels: ['规划中', '实现中', '已实现', '已放弃'],
      datasets: [
        {
          backgroundColor: [
            getStyle('--secondary'),
            getStyle('--primary'),
            getStyle('--success'),
            getStyle('--danger')
          ],
          data: [16, 3, 10, 1]
        }
      ]
    }, {responsive: true, maintainAspectRatio: false})
  }
}
</script>
