<template>
  <div v-bind:class="{bordaGreen: bordaGreen, bordaRed: bordaRed}" class="card1">
    <h1><b>{{ nomeDisplay }}</b></h1>
    <div class="led">
      <div>
        <table class="tabela">
          <tr>
            <th>LED 1</th>
            <th>
              <v-icon v-if="ficaVermelho[0]" color="#000000">mdi-white-balance-sunny</v-icon>
              <v-icon v-if="ficaVerde[0]" color="#ffffff">mdi-white-balance-sunny</v-icon>
            </th>
          </tr>
          <tr>
            <th>LED 2</th>
            <th>
              <v-icon v-if="ficaVermelho[1]" color="#000000">mdi-white-balance-sunny</v-icon>
              <v-icon v-if="ficaVerde[1]" color="#ffffff">mdi-white-balance-sunny</v-icon>
            </th>
          </tr>
          <tr>
            <th>LED 3</th>
            <th>
              <v-icon v-if="ficaVermelho[2]" color="#000000">mdi-white-balance-sunny</v-icon>
              <v-icon v-if="ficaVerde[2]" color="#ffffff">mdi-white-balance-sunny</v-icon>
            </th>
          </tr>
          <tr>
            <th>LED 4</th>
            <th>
              <v-icon v-if="ficaVermelho[3]" color="#000000">mdi-white-balance-sunny</v-icon>
              <v-icon v-if="ficaVerde[3]" color="#ffffff">mdi-white-balance-sunny</v-icon>
            </th>
          </tr>
          <tr>
            <th>LED 5</th>
            <th>
              <v-icon v-if="ficaVermelho[4]" color="#000000">mdi-white-balance-sunny</v-icon>
              <v-icon v-if="ficaVerde[4]" color="#ffffff">mdi-white-balance-sunny</v-icon>
            </th>
          </tr>
        </table>
      </div>
    </div>
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

  props: {
    nome: {type: String, default: "maquina - 1"},
    nomeDisplay: {type: String, default: "maquina - 1"}
  },

  data() {
    return {
      // mudança de icones
      ficaVerde: [false, false, false, false, false],
      ficaVermelho: [true, true, true, true, true],
      bordaRed: true,
      bordaGreen: false,

      // Array will be automatically processed with visualization.arrayToDataTable function
      chartTemp0: [
        ['Label', 'Value'],
        ['Temp 0', 0]
      ],
      chartOTemp0: {
        width: 450, height: 150,
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
        width: 450, height: 150,
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
        width: 450, height: 150,
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
        width: 450, height: 150,
        greenFrom: 370, greenTo: 377.5,
        redFrom: 392.5, redTo: 400,
        yellowFrom: 377.5, yellowTo: 392.5,
        minorTicks: 5, min: 370, max: 400
      }
    }
  },

  mqtt: {
    'aut_lab/#': function (val, topic) {
      if ('aut_lab/' + this.nome + '/temperatura/temp0' === topic) {
        let temp0 = String.fromCharCode.apply(null, val)
        console.log(temp0)
        console.log(topic)
        this.chartTemp0 = [
          ['Label', 'Value'],
          ['Temp 0', Number(temp0)]]
      }
      if ('aut_lab/' + this.nome + '/temperatura/temp1' === topic) {
        let temp1 = String.fromCharCode.apply(null, val)
        console.log(temp1)
        console.log(topic)
        this.chartTemp1 = [
          ['Label', 'Value'],
          ['Temp 1', Number(temp1)]]
      }
      if ('aut_lab/' + this.nome + '/correntes/corrente0' === topic) {
        let corrente = String.fromCharCode.apply(null, val)
        console.log(corrente)
        console.log(topic)
        this.chartCorrente = [
          ['Label', 'Value'],
          ['Corrente', Number(corrente)]]
      }
      if ('aut_lab/' + this.nome + '/tensoes/tensao0' === topic) {
        let tensao = String.fromCharCode.apply(null, val)
        console.log(tensao)
        console.log(topic)
        this.chartTensao = [
          ['Label', 'Value'],
          ['Tensão', Number(tensao)]]
      }
      if ('aut_lab/' + this.nome + '/leds/led0' === topic) {
        let led0 = JSON.parse(String.fromCharCode.apply(null, val))
        console.log(led0)
        console.log(topic)
        if (led0 === 0) {
          this.ficaVermelho[0] = true
          this.ficaVerde[0] = false
        } else {
          this.ficaVermelho[0] = false
          this.ficaVerde[0] = true
        }
      }
      if ('aut_lab/' + this.nome + '/leds/led1' === topic) {
        let led1 = JSON.parse(String.fromCharCode.apply(null, val))
        console.log(led1)
        console.log(topic)
        if (led1 === 0) {
          this.ficaVermelho[1] = true
          this.ficaVerde[1] = false
        } else {
          this.ficaVermelho[1] = false
          this.ficaVerde[1] = true
        }
      }
      if ('aut_lab/' + this.nome + '/leds/led2' === topic) {
        let led2 = JSON.parse(String.fromCharCode.apply(null, val))
        console.log(led2)
        console.log(topic)
        if (led2 === 0) {
          this.ficaVermelho[2] = true
          this.ficaVerde[2] = false
        } else {
          this.ficaVermelho[2] = false
          this.ficaVerde[2] = true
        }
      }
      if ('aut_lab/' + this.nome + '/leds/led3' === topic) {
        let led3 = JSON.parse(String.fromCharCode.apply(null, val))
        console.log(led3)
        console.log(topic)
        if (led3 === 0) {
          this.ficaVermelho[3] = true
          this.ficaVerde[3] = false
        } else {
          this.ficaVermelho[3] = false
          this.ficaVerde[3] = true
        }
      }
      if ('aut_lab/' + this.nome + '/leds/led4' === topic) {
        let led4 = JSON.parse(String.fromCharCode.apply(null, val))
        console.log(led4)
        console.log(topic)
        if (led4 === 0) {
          this.ficaVermelho[4] = true
          this.ficaVerde[4] = false
        } else {
          this.ficaVermelho[4] = false
          this.ficaVerde[4] = true
        }
      }
      if ('aut_lab/' + this.nome + '/alarmes/alarme0' === topic) {
        let alarme0 = JSON.parse(String.fromCharCode.apply(null, val))
        console.log(alarme0)
        console.log(topic)
        if (alarme0 === 0) {
          this.bordaRed = true
          this.bordaGreen = false
        } else {
          this.bordaRed = false
          this.bordaGreen = true
        }
      }
    },
  },
}
</script>

<style scoped>
.centro {
  display: flex;
  flex-wrap: wrap;
  margin: auto;
}

h1, table {
  color: black;
}

.card1 {
  width: 20%;
  border: 5px white solid;
  border-radius: 10px;
  display: inline-block;
  float: top;
}

.bordaGreen {
  border-color: #008000;
  background-color: #49fd4b;
}

.bordaRed {
  border-color: #ff0000;
  background-color: #fd4444;
  animation: pisca 1s ease-in-out infinite alternate;
}

@keyframes pisca {
    from {
      border-color: #ff0000;
      background-color: #fd4444;
    }

    to {
      border-color: #ff0000;
      background-color: #ff7d7d;
    }
}

.led {
  margin: auto;
  text-align: center;
}

.tabela {
  margin: auto;
  width: 250px;
}

</style>