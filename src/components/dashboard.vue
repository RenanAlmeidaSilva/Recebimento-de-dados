<template>
  <div>
    <h1><b>Máquina 1</b></h1>
    <br><br>
    <div class="led">
      <!--
      <div class="linha">
        <p>
          LED 1
          &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;
          <v-icon color="#ff0000">mdi-white-balance-sunny</v-icon>
        </p>
      </div>
      -->
      <div class="tabela">
        <table>
          <tr>
            <th>LED 1</th>
            <th><v-icon color="#ff0000">mdi-white-balance-sunny</v-icon></th>
          </tr>
          <tr>
            <th>LED 2</th>
            <th><v-icon color="#ff0000">mdi-white-balance-sunny</v-icon></th>
          </tr>
          <tr>
            <th>LED 3</th>
            <th><v-icon color="#ff0000">mdi-white-balance-sunny</v-icon></th>
          </tr>
          <tr>
            <th>LED 4</th>
            <th><v-icon color="#ff0000">mdi-white-balance-sunny</v-icon></th>
          </tr>
          <tr>
            <th>LED 5</th>
            <th><v-icon color="#ff0000">mdi-white-balance-sunny</v-icon></th>
          </tr>
        </table>
      </div>

    </div>
    <br><br>
      <div class="centro">
      <div class="centro">
        <GChart
          :settings="{ packages: ['Gauge'] }"
          type="Gauge"
          :data="chartTemp0"
          :options="chartOTemp0"
        />
      </div>
      <div class="centro">
        <GChart
          :settings="{ packages: ['Gauge'] }"
          type="Gauge"
          :data="chartTemp1"
          :options="chartOTemp1"
        />
      </div>
      <div class="centro">
        <GChart
          :settings="{ packages: ['Gauge'] }"
          type="Gauge"
          :data="chartCorrente"
          :options="chartOCorrente"
      />
      </div>
      <div class="centro">
        <GChart
          :settings="{ packages: ['Gauge'] }"
          type="Gauge"
          :data="chartTensao"
          :options="chartOTensao"
      />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "dashboard",
  data() {
    return {
      // Array will be automatically processed with visualization.arrayToDataTable function
      chartTemp0: [
        ['Label', 'Value'],
        ['Temp 0', 0]
      ],
      chartOTemp0: {
        width: 400, height: 150,
        greenFrom: 18, greenTo: 26,
        redFrom: 42, redTo: 50,
        yellowFrom: 26, yellowTo: 42,
        minorTicks: 5, min: 18, max: 50
      },
      chartTemp1: [
        ['Label', 'Value'],
        ['Temp 1', 0]
      ],
      chartOTemp1: {
        width: 400, height: 150,
        greenFrom: 18, greenTo: 26,
        redFrom: 42, redTo: 50,
        yellowFrom: 26, yellowTo: 42,
        minorTicks: 5, min: 18, max: 50
      },
      chartCorrente: [
        ['Label', 'Value'],
        ['Corrente', 0]
      ],
      chartOCorrente: {
        width: 400, height: 150,
        greenFrom: 5, greenTo: 6.25,
        redFrom: 8.75, redTo: 10,
        yellowFrom: 6.25, yellowTo: 8.75,
        minorTicks: 5, min: 5, max: 10
      },
      chartTensao: [
        ['Label', 'Value'],
        ['Tensão', 0]
      ],
      chartOTensao: {
        width: 400, height: 150,
        greenFrom: 370, greenTo: 377.5,
        redFrom: 392.5, redTo: 400,
        yellowFrom: 377.5, yellowTo: 392.5,
        minorTicks: 5, min: 370, max: 400
      }
    }
  }
}
</script>

<style scoped>
.centro {
  display: inline-block;
}

.led {
  margin: auto;
  text-align: center;
}

.linha {
  margin: auto;
  display: inline-block;
}

.tabela {
  border: 4px red solid;
  margin: auto;
  width: 575px;
  padding: 10px;
}
</style>