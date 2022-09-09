<template>
  <div class="q-pa-md items-center element" :class="{ blur: disabled, 'current': model === 'one', 'alternative': model === 'two' }">
    <q-toolbar class="rounded-borders vertical-middle" style="height: 63px">
      <q-toolbar-title class="text-center">
        <img src="@/assets/btc_sustainable.svg" alt="make bitcoin nachhalitg" style="height: 34px">
      </q-toolbar-title>
    </q-toolbar>

    <div class="row justify-center items-center q-mt-lg q-mb-md">
      <q-btn-toggle
          @click="warnDisabled"
          id="toggle-btn"
          v-model="model"
          class="my-custom-toggle bi-border-all"
          push
          no-caps
          rounded
          toggle-color="grey-9"
          unelevated
          color="white"
          text-color="grey-9"
          :options="options"
      />
    </div>

    <div class="row justify-center items-center q-mt-lg" v-if="model === 'one'">
      <q-card dark class="my-card" style="width: 80%; backdrop-filter: blur(8px)">
        <q-card-section class="row justify-center items-center q-mt-lg">
          <q-circular-progress
              show-value
              font-size="20px"
              :value="percentage"
              size="200px"
              :thickness="0.15"
              color="red"
              track-color="grey-8"
              class="q-ma-md"
          >
            {{ btcData }} KWh
          </q-circular-progress>
          <q-icon class="q-ma-md" name="info" size="26px" outlined>
            <q-tooltip>
              Abgerufen am 31. August 2022
            </q-tooltip>
          </q-icon>
          <br>
          <h6> Der derzeitige tägliche BTC-Stromverbrauch <br> entspricht <strong>{{percentage}} %</strong> des täglichen <br>Stromverbrauchs in ganz Deutschland. </h6>
        </q-card-section>
      </q-card>
    </div>

    <div class="row justify-center items-center q-mt-lg" v-if="model === 'two'">
    <q-card dark class="my-card" style="width: 80%">

      <q-card-section class="row justify-center items-center q-mt-lg">
          <q-circular-progress
              show-value
              font-size="20px"
              :value="altpercentage"
              size="200px"
              :thickness="0.15"
              color="green"
              track-color="grey-8"
              class="q-ma-md"
          >
            {{ altbtcData }} KWh
          </q-circular-progress>
          <q-icon class="q-ma-md" name="info" size="26px" outlined>
            <q-tooltip>
              Abgerufen am 31. August 2022
            </q-tooltip>
          </q-icon>
          <br>
          <h6> Der alternative tägliche BTC-Stromverbrauch <br> könnte bei <strong class="text-green6">{{altpercentage}} %</strong> des täglichen <br>Stromverbrauchs in ganz Deutschland liegen. </h6>
        </q-card-section>
      </q-card>
    </div>

    <div class="row justify-center items-center">
      <div class="q-gutter-md q-mt-lg" style="width: 80%">
        <q-separator class="q-mt-lg" color="grey-6" /><br>
        <div v-if="model === 'one'">
          <div style="text-align: center">
            <h5 style="margin: 0">Mit dem aktuellen täglichen Stromverbrauch könnten</h5>
          </div>
          <div class="row justify-center items-center" style="text-align: center">
            <div class="col" style="text-align: center">
              <q-card dark class="my-card bg-dark">
                <q-card-section>
                  <q-icon name="home" size="56px" />
                </q-card-section>
                <q-card-section class="q-pt-none">
                  <h6 class="text-red-6" style="margin: 2px">{{cardContent[0].consumption.replace(/\B(?=(\d{3})+(?!\d))/g, ".")}}</h6>
                  deutsche Haushalte ein Jahr versorgt werden.
                </q-card-section>
              </q-card>
            </div>
            <div class="col q-ma-lg" style="text-align: center">
              <q-card dark class="my-card bg-dark">
                <q-card-section>
                  <q-icon name="kitchen" size="56px" />
                </q-card-section>
                <q-card-section class="q-pt-none">
                  <h6 class="text-red-6" style="margin: 2px">{{cardContent[2].consumption.replace(/\B(?=(\d{3})+(?!\d))/g, ".")}}</h6>
                  Kühlschränke ein Jahr lang betrieben werden.
                </q-card-section>
              </q-card>
            </div>
            <div class="col" style="text-align: center">
              <q-card dark class="my-card bg-dark">
                <q-card-section>
                  <q-icon name="electric_car" size="56px" />
                </q-card-section>
                <q-card-section class="q-pt-none">
                  <h6 class="text-red-6" style="margin: 2px">{{cardContent[1].consumption.replace(/\B(?=(\d{3})+(?!\d))/g, ".")}}</h6>
                  E-Autos ein Jahr lang gefahren werden.
                </q-card-section>
              </q-card>
            </div>
          </div>
        </div>
        <div v-if="model === 'two'">
          <div style="text-align: center">
            <h5 style="margin: 0">Mit einer alternativen Implementierung könnten</h5>
          </div>
          <div class="row justify-center items-center" style="text-align: center">
            <div class="col" style="text-align: center">
              <q-card dark class="my-card bg-dark">
                <q-card-section>
                  <q-icon name="electric_bolt" size="56px" />
                </q-card-section>
                <q-card-section class="q-pt-none">
                  <h6 class="text-green-6" style="margin: 2px">95%</h6>
                  des aktuellen Stromverbrauchs eingespart werden.
                </q-card-section>
              </q-card>
            </div>
            <div class="col q-ma-lg" style="text-align: center">
              <q-card dark class="my-card bg-dark">
                <q-card-section>
                  <q-icon name="energy_savings_leaf" size="56px" />
                </q-card-section>
                <q-card-section class="q-pt-none">
                  <h6 class="text-green-6" style="margin: 2px">124,56 TWh</h6>
                  vom jährlichen Stromverbrauch eingespart werden.
                  <!--  https://digiconomist.net/bitcoin-energy-consumption  -->
                </q-card-section>
              </q-card>
            </div>
            <div class="col" style="text-align: center">
              <q-card dark class="my-card bg-dark">
                <q-card-section>
                  <q-icon name="wind_power" size="56px" />
                </q-card-section>
                <q-card-section class="q-pt-none">
                  <h6 class="text-green-6" style="margin: 2px">{{ btcCo2Diff.replace(/\B(?=(\d{3})+(?!\d))/g, ".") }} kgCO2</h6>
                  bei der täglichen Nutzung eingespart werden.
                </q-card-section>
              </q-card>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="row justify-center items-center q-mt-lg">
      <q-card dark class="bg-dark rounded my-card" style="width: 80%">
        <q-card-section class="row justify-center q-mt-lg">
            <div class="col q-mr-md" v-if="model === 'one'">
              <h5 style="margin: 0px">Aktueller Energieverbrauch</h5>
              <small>Unter Verwendung der klassischen
                Proof-of-Work-Blockchain.</small>
            </div>
          <div class="col" v-if="model === 'two'">
            <h5 style="margin: 0px">Alternativer Energieverbrauch</h5>
            <small>Unter Verwendung einer alternativen
              Proof-of-Stake-Blockchain.</small>
          </div>
          <div class="col">
            <q-list dark bordered separator style="max-width: 318px" v-if="model === 'one'">
              <q-item v-ripple>
                <q-item-section>
                  <q-item-label overline>Stromverbrauch (letzte 24h)</q-item-label>
                  <q-item-label class="text-red-5">{{btcData}} KWh</q-item-label>
                </q-item-section>
              </q-item>
              <q-item v-ripple>
                <q-item-section>
                  <q-item-label overline>Emissionen (letzte 24h)</q-item-label>
                  <q-item-label class="text-red-5">{{btcCo2}} kgCO2</q-item-label>
                </q-item-section>
              </q-item>
              <q-item v-ripple>
                <q-item-section>
                  <q-item-label overline>Stromverbrauch pro Transaktion</q-item-label>
                  <q-item-label class="text-red-5">{{btcOutKwh}} KWh</q-item-label>
                </q-item-section>
              </q-item>
              <q-item v-ripple>
                <q-item-section>
                  <q-item-label overline>Emissionen pro Transaktion</q-item-label>
                  <q-item-label class="text-red-5">{{btcOutCo2}} kgCO2</q-item-label>
                </q-item-section>
              </q-item>
            </q-list>

            <q-list dark bordered separator style="max-width: 318px" v-if="model === 'two'">
              <q-item v-ripple>
                <q-item-section>
                  <q-item-label overline>Stromverbrauch (letzte 24h)</q-item-label>
                  <q-item-label class="text-green-6">{{altbtcData}} KWh</q-item-label>
                </q-item-section>
              </q-item>
              <q-item v-ripple>
                <q-item-section>
                  <q-item-label overline>Emissionen (letzte 24h)</q-item-label>
                  <q-item-label class="text-green-6">{{altbtcCo2}} kgCO2</q-item-label>
                </q-item-section>
              </q-item>
              <q-item v-ripple>
                <q-item-section>
                  <q-item-label overline>Stromverbrauch pro Transaktion</q-item-label>
                  <q-item-label class="text-green-6">{{altbtcOutKwh}} KWh</q-item-label>
                </q-item-section>
              </q-item>
              <q-item v-ripple>
                <q-item-section>
                  <q-item-label overline>Emissionen pro Transaktion</q-item-label>
                  <q-item-label class="text-green-6">{{altbtcOutCo2}} kgCO2</q-item-label>
                </q-item-section>
              </q-item>
            </q-list>
          </div>
        </q-card-section>
      </q-card>
    </div>
<br>
    <div class="row justify-center items-center q-mt-lg">
      <q-card dark class="bg-dark rounded my-card" style="width: 80%">
        <q-card-section class="row q-ma-sm">
          <h5 style="margin: 0">Wieso ist der Bitcoin nicht nachhaltig?</h5>
        </q-card-section>
      </q-card>
    </div>

    <div class="row justify-center items-center q-mt-lg">
      <q-card dark class="bg-dark rounded my-card" style="width: 80%">
        <q-card-section class="row q-ma-sm">
          <h5 style="margin: 0">Wie kann man den Bitcoin nachhaltiger gestalten?</h5>
        </q-card-section>
      </q-card>
    </div>
    <div>
      <q-tabs no-caps active-color="grey-9" indicator-color="transparent" class="text-white q-mt-lg" v-model="tab">
        <q-tab name="images" label="Impressum" />
        <q-tab name="videos" label="Quellen" />
        <q-tab name="articles" label="Grafiken" />
      </q-tabs>
    </div>
  </div>
</template>

<script>
import {onMounted, ref} from 'vue'
import axios from "axios";

const options = [
  {label: 'Aktuell', value: 'one'},
  {label: 'Alternativ', value: 'two'}
]

const btcData = ref(null);
const btcCo2 = ref(null);
const btcOutKwh = ref(null);
const btcOutCo2 = ref(null);

const altbtcData = ref(null);
const altbtcCo2 = ref(null);
const altbtcOutKwh = ref(null);
const altbtcOutCo2 = ref(null);

const btcCo2Diff = ref(null);

const altpercentage = ref(null);
const percentage = ref(null);

const cardContent = ref([
  {
    title: "Haushalt",
    icon: "home",
    consumption: "",
    label: `Mit dem aktuellen täglichen Stromverbrauch könnten ${(btcData.value / 3106).toFixed(0).toString()} deutsche Haushalte ein Jahr versorgt werden.`,
    //https://www.destatis.de/DE/Themen/Gesellschaft-Umwelt/Umwelt/UGR/private-haushalte/Tabellen/stromverbrauch-haushalte.html
  },
  {
    title: "E-Autos",
    icon: "car",
    consumption: "",
    //https://www.bussgeldkatalog.org/verbrauch-elektroautos/#wie_hoch_ist_der_stromverbrauch_bei_einem_elektroauto_pro_jahr
  },
  {
    title: "Kühlschrank",
    icon: "kitchen",
    consumption: "",
    //https://www.co2online.de/energie-sparen/strom-sparen/strom-sparen-stromspartipps/kuehlschrank/#:~:text=Fakten%20zum%20Stromverbrauch%20eines%20K%C3%BChlschranks,etwa%2029%20bis%2040%20Euro.
  }
]);

export default {
  setup () {
    async function getData() {
      try {
        const response = await axios.get(
            "https://digiconomist.net/wp-json/mo/v1/bitcoin/stats/20220827"
        );
        // JSON responses are automatically parsed.
        btcData.value = response.data[0]["24hr_kWh"];
        btcCo2.value = response.data[0]["24hr_kgCO2"];
        btcOutKwh.value = response.data[0]["Output_kWh"];
        btcOutCo2.value = response.data[0]["Output_kgCO2"];

        altbtcData.value = ((btcData.value * 0.005).toFixed(0)).toString();
        altbtcCo2.value = (btcCo2.value * 0.005).toString();
        altbtcOutKwh.value = (btcOutKwh.value * 0.005).toString();
        altbtcOutCo2.value = (btcOutCo2.value * 0.005).toString();

        percentage.value = (Number(btcData.value) / 922739726 * 100).toFixed(2);
        altpercentage.value = (Number(btcData.value) / 922739726 * 100 * 0.02).toFixed(2);

        cardContent.value[0].consumption = (btcData.value / 3106).toFixed(0).toString();
        cardContent.value[1].consumption = (btcData.value / 2250).toFixed(0).toString();
        cardContent.value[2].consumption = (btcData.value / 107.5).toFixed(0).toString();

        btcCo2Diff.value = (btcCo2.value - altbtcCo2.value).toFixed(0).toString();
      } catch (error) {
        console.log(error);
      }
    }

    onMounted(() => {
      getData();
    });

    return {
      value: 80,
      tab: ref(''),
      model: ref('one'),
      btcData,
      btcCo2,
      btcOutCo2,
      btcOutKwh,
      percentage,
      altbtcCo2,
      altbtcOutCo2,
      altbtcOutKwh,
      altbtcData,
      altpercentage,
      options,
      cardContent,
      btcCo2Diff
    }
  },
  data() {
    return {
      disabled: false
    }
  },
  methods: {
    warnDisabled() {
      this.disabled = true
      console.log(this.disabled)
      setTimeout(() => {
        this.disabled = false
        console.log(this.disabled)
      }, 1000)
    }
  }
}
</script>
<style>
body {
  animation: gradient 15s ease infinite;
  height: 100vh;
  border-radius: 20px;
  backdrop-filter: blur(5px);
  color: ghostwhite;
  font-family: Arial, Helvetica, sans-serif;
  zoom: 120%;
}
.current {
  background: #5b5b5b;
  background-image: radial-gradient(farthest-side at bottom left, rgb(176, 111, 111), transparent), radial-gradient(farthest-corner at bottom right, rgb(63, 63, 64), transparent 400px);
}
.alternative {
  background: #537a57;
  background-image: radial-gradient(farthest-side at bottom left, rgb(176, 143, 111), transparent), radial-gradient(farthest-corner at bottom right, rgb(172, 252, 180), transparent 400px);
}
@keyframes gradient {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}
@keyframes image_blur {
  0% { -webkit-filter: blur(30px);}
  50% { -webkit-filter: blur(60px);}
  100% { -webkit-filter: blur(0px);}
}
div.blur {
  animation: image_blur 1s;
}
::-webkit-scrollbar {
  width: 8px;
  height: 8px;
}

::-webkit-scrollbar-track {
  background: transparent;
}

::-webkit-scrollbar-thumb {
  background: #545454;
  border-radius: 4px;
}

::-webkit-scrollbar-thumb:hover {
  background: rgba(#58c6b2, 0.8);
}
</style>