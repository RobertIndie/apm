<script>
import { Line } from 'vue-chartjs'
import { getStyle, hexToRgba } from '@coreui/coreui/dist/js/coreui-utilities'
import { CustomTooltips } from '@coreui/coreui-plugin-chartjs-custom-tooltips'

function random (min, max) {
  return Math.floor(Math.random() * (max - min + 1) + min)
}

export default {
  extends: Line,
  props: ['height'],
  mounted () {
    const brandSuccess = getStyle('--success') || '#4dbd74'
    const brandInfo = getStyle('--info') || '#20a8d8'
    const brandDanger = getStyle('--danger') || '#f86c6b'

    let elements = 27
    const data1 = []
    const data2 = []
    const data3 = []

    for (let i = 0; i <= elements; i++) {
      data1.push(random(0, 10))
      data2.push(random(0, 3))
    }
    this.renderChart({
      labels: ['周一', '周二', '周三', '周四', '周五', '周六', '周日', '周一', '周二', '周三', '周四', '周五', '周六', '周日'],
      datasets: [
        {
          label: '规模',
          backgroundColor: hexToRgba(brandInfo, 10),
          borderColor: brandInfo,
          pointHoverBackgroundColor: '#fff',
          borderWidth: 2,
          data: data1
        },
        {
          label: '任务',
          backgroundColor: 'transparent',
          borderColor: brandSuccess,
          pointHoverBackgroundColor: '#fff',
          borderWidth: 2,
          data: data2
        }
      ]
    }, {
      tooltips: {
        enabled: false,
        custom: CustomTooltips,
        intersect: true,
        mode: 'index',
        position: 'nearest',
        callbacks: {
          labelColor: function (tooltipItem, chart) {
            return { backgroundColor: chart.data.datasets[tooltipItem.datasetIndex].borderColor }
          }
        }
      },
      maintainAspectRatio: false,
      legend: {
        display: false
      },
      scales: {
        xAxes: [{
          gridLines: {
            drawOnChartArea: false
          }
        }],
        yAxes: [{
          ticks: {
            beginAtZero: true,
            maxTicksLimit: 5,
            stepSize: Math.ceil(15 / 5),
            max: 15
          },
          gridLines: {
            display: true
          }
        }]
      },
      elements: {
        point: {
          radius: 0,
          hitRadius: 10,
          hoverRadius: 4,
          hoverBorderWidth: 3
        }
      }
    })
  }
}
</script>
