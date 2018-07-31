<script>
import { Line } from 'vue-chartjs'
import { CustomTooltips } from '@coreui/coreui-plugin-chartjs-custom-tooltips'
import { hexToRgba } from '@coreui/coreui/dist/js/coreui-utilities'

export default {
  name: 'countBurnChart',
  components: {
    hexToRgba,
    CustomTooltips
  },
  extends: Line,
  mounted () {
    this.renderChart(
      {
        labels: ['周一', '周二', '周三', '周四', '周五', '周六', '周日'],
        datasets: [
          {
            label: '基准线',
            backgroundColor: hexToRgba('#20a8d8',0),
            borderColor: '#20a8d8',
            data: [42, 35, 28, 21, 14, 7, 0]
          },
          {
            label: '规模',
            backgroundColor: hexToRgba('#E46651', 90),
            data: [42, 35, 25, 15, 13, 5, 0]
          }
        ]
      },
      {
        responsive: true,
        maintainAspectRatio: false,
        tooltips: {
          enabled: false,
          custom: CustomTooltips,
          intersect: true,
          mode: 'index',
          position: 'nearest',
          callbacks: {
            labelColor: function (tooltipItem, chart) {
              return { backgroundColor: chart.data.datasets[tooltipItem.datasetIndex].backgroundColor }
            }
          }
        },
        legend: {
          display: false
        }
      }
    )
  }
}
</script>
