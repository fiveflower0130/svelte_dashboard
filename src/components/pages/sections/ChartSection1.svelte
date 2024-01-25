<script>
  import MDBCard from 'mdbsvelte/src/MDBCard.svelte';
  import MDBCardHeader from 'mdbsvelte/src/MDBCardHeader.svelte';
  import MDBListGroup from 'mdbsvelte/src/MDBListGroup.svelte';
  import MDBListGroupItem from 'mdbsvelte/src/MDBListGroupItem.svelte';
  import MDBCardBody from 'mdbsvelte/src/MDBCardBody.svelte';
  import MDBIcon from 'mdbsvelte/src/MDBIcon.svelte';
  import MDBRow from 'mdbsvelte/src/MDBRow.svelte';
  import MDBCol from 'mdbsvelte/src/MDBCol.svelte';
  import MDBBadge from 'mdbsvelte/src/MDBBadge.svelte';

  import Bar from 'svelte-chartjs/src/Bar.svelte';
  import Pie from 'svelte-chartjs/src/Pie.svelte';

  const dataBar = {
    labels: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul'],
    datasets: [
      {
        label: 'On time 批數',
        data: [12, 39, 3, 50, 2, 32, 84],
        backgroundColor: 'rgba(245, 74, 85, 0.5)',
        borderWidth: 1
      },
      {
        label: 'SOD Risk 批數',
        data: [56, 24, 5, 16, 45, 24, 8],
        backgroundColor: 'rgba(90, 173, 246, 0.5)',
        borderWidth: 1
      },
      {
        label: 'Delay 批數',
        data: [12, 25, 54, 3, 15, 44, 3],
        backgroundColor: 'rgba(245, 192, 50, 0.5)',
        borderWidth: 1
      }
    ]
  };

  const barChartOptions = {
    responsive: true,
    maintainAspectRatio: false,
    scales: {
      xAxes: [
        {
          barPercentage: 1,
          gridLines: {
            display: true,
            color: 'rgba(0, 0, 0, 0.1)'
          }
        }
      ],
      yAxes: [
        {
          gridLines: {
            display: true,
            color: 'rgba(0, 0, 0, 0.1)'
          },
          ticks: {
            beginAtZero: true
          }
        }
      ]
    }
  };

  // implemented a stacked bar chart data and options, display inline values in a stacked barchart.

  const dataStackedBar = {
    labels: [
      ['BRCM', 'Baily'],
      ['Socionext', 'Taurus'],
      ['MTK', 'A60499'],
      ['BRM', 'JR2-7P7M'],
      ['Qualcomm', 'FO-IL CL L1 DTC'],
      ['BOSCH', 'Maokung'],
      ['Intel', 'BD Wafer'],
      ['WINBOND', 'WTCMF00QSS9E'],
      ['BRCM', 'TH6'],
      ['CISCO', 'LaMP'],
      ['Qualcomm', 'APD1']
    ],
    datasets: [
      {
        label: 'On Time批數',
        backgroundColor: 'rgba(90, 173, 246, 0.5)',
        data: [2, 0, 6, 1, 1, 0, 2, 2, 1, 4, 6],
        hoverBorderWidth: 2,
        hoverBorderColor: 'lightgrey',
        textColor: 'black'
      },
      {
        label: 'SOD Risk',
        backgroundColor: 'rgba(245, 192, 50, 0.5)',
        data: [0, 2, 0, 2, 1, 0, 0, 0, 1, 0, 0],
        hoverBorderWidth: 2,
        hoverBorderColor: 'lightgrey',
        textColor: 'black'
      },
      {
        label: 'Delay批數',
        backgroundColor: 'rgba(245, 74, 85, 0.5)',
        data: [1, 0, 0, 0, 0, 1, 0, 0, 2, 0, 0],
        hoverBorderWidth: 2,
        hoverBorderColor: 'lightgrey',
        textColor: 'black'
      }
    ]
  };
  const stackedBarChartOptions = {
    responsive: true,
    maintainAspectRatio: false,
    scales: {
      xAxes: [
        {
          stacked: true,
          barPercentage: 0.6,
          gridLines: {
            display: true,
            color: 'rgba(0, 0, 0, 0.1)'
          },
          ticks: {
            fontSize: 9,
            fontString: 'bold'
          }
        }
      ],
      yAxes: [
        {
          stacked: true,
          display: true,
          gridLines: {
            display: true,
            color: 'rgba(0, 0, 0, 0.1)'
          },
          ticks: {
            beginAtZero: true,
            max: 8,
            min: 0
          }
        }
      ]
    },
    animation: {
      onComplete: function (animation) {
        const ctx = this.chart.ctx;
        ctx.font = Chart.helpers.fontString(
          Chart.defaults.global.defaultFontSize,
          'normal',
          Chart.defaults.global.defaultFontFamily
        );
        ctx.fillStyle = this.chart.config.options.defaultFontColor;
        ctx.textAlign = 'center';
        ctx.textBaseline = 'bottom';

        this.data.datasets.forEach(function (dataset) {
          for (let i = 0; i < dataset.data.length; i++) {
            console.log(dataset.data[i]);
            const model =
              dataset._meta[Object.keys(dataset._meta)[0]].data[i]._model;
            if (dataset.data[i] > 0) {
              ctx.fillText(dataset.data[i], model.x, model.y + model.y / 10);
            }
          }
        });
      }
    }
    // tooltips: {
    //   mode: 'index',
    //   intersect: false
    // }
  };

  const dataPie = {
    labels: [
      'BRCM Baily',
      'Socionext Taurus',
      'MTK A60499',
      'BRM JR2-7P7M',
      'Qualcomm FO-IL CL L1 DTC',
      'BOSCH Maokung',
      'Intel BD Wafer',
      'WINBOND WTCMF00QSS9E',
      'BRCM TH6',
      'CISCO LaMP',
      'Qualcomm APD1'
    ],
    datasets: [
      {
        data: [3, 2, 6, 3, 2, 1, 2, 2, 4, 4, 6],
        backgroundColor: [
          '#F7464A',
          '#46BFBD',
          '#FDB45C',
          '#949FB1',
          '#4D5360',
          '#ac64ad',
          '#ffff56',
          '#63ff7a',
          '#36a2eb',
          '#cc65fe',
          '#7b56ff'
        ],
        hoverBackgroundColor: [
          '#FF5A5E',
          '#5AD3D1',
          '#FFC870',
          '#A8B3C5',
          '#616774',
          '#da92db',
          '#ffce56',
          '#73ff63',
          '#36b2eb',
          '#dd65fe',
          '#6756ff'
        ]
      }
    ]
  };

  const pieChartOptions = {
    responsive: true,
    maintainAspectRatio: false, // 保持图表原有比例
    animation: {
      onComplete: function () {
        const ctx = this.chart.ctx;
        const datasets = this.data.datasets;
        const meta = this.chart.getDatasetMeta(0);
        const midX = this.chart.width / 2;
        const midY = this.chart.height / 2;
        const radius = this.chart.height / 2;

        ctx.fillStyle = 'black';
        const textSize = this.chart.width / 30;
        ctx.font = textSize + 'px Verdana';

        meta.data.forEach((segment, i) => {
          const value = datasets[0].data[i];
          const startAngle = segment._model.startAngle;
          const endAngle = segment._model.endAngle;
          const middleAngle = startAngle + (endAngle - startAngle) / 2;

          const posX = (radius / 2) * Math.cos(middleAngle) + midX;
          const posY = (radius / 2) * Math.sin(middleAngle) + midY;

          const w_offset = ctx.measureText(value).width;
          const h_offset = textSize * 4;

          ctx.fillText(value, posX - w_offset, posY + h_offset);
        });
      }
    }
  };

  const pieChartPlugins = {};
</script>

<MDBRow class="mb-4">
  <MDBCol md="8" class="mb-4">
    <MDBCard class="mb-4">
      <MDBCardHeader>客戶設備批數統計圖</MDBCardHeader>
      <MDBCardBody>
        <Bar
          data={dataStackedBar}
          height={580}
          options={stackedBarChartOptions}
        />
      </MDBCardBody>
    </MDBCard>
  </MDBCol>
  <MDBCol md="4" class="mb-4">
    <MDBCard class="mb-4">
      <MDBCardHeader>批數統計圖</MDBCardHeader>
      <MDBCardBody>
        <Pie
          data={dataPie}
          height={580}
          options={pieChartOptions}
          plugins={pieChartPlugins}
        />
      </MDBCardBody>
    </MDBCard>
    <!-- <MDBCard class="mb-4">
      <MDBCardBody>
        <MDBListGroup class="list-group-flush">
          <MDBListGroupItem>
            On Time
            <MDBBadge color="success-color" pill class="float-right">
              22%
              <MDBIcon icon="arrow-up" class="ml-1" />
            </MDBBadge>
          </MDBListGroupItem>
          <MDBListGroupItem>
            SOD Risk
            <MDBBadge color="danger-color" pill class="float-right">
              5%
              <MDBIcon icon="arrow-down" class="ml-1" />
            </MDBBadge>
          </MDBListGroupItem>
          <MDBListGroupItem>
            Delay 批數
            <MDBBadge color="primary-color" pill class="float-right">
              14
            </MDBBadge>
          </MDBListGroupItem>
          <MDBListGroupItem>
            總批數
            <MDBBadge color="primary-color" pill class="float-right">
              123
            </MDBBadge>
          </MDBListGroupItem>
          <MDBListGroupItem>
            通報數
            <MDBBadge color="primary-color" pill class="float-right">
              8
            </MDBBadge>
          </MDBListGroupItem>
        </MDBListGroup>
      </MDBCardBody>
    </MDBCard> -->
  </MDBCol>
</MDBRow>
