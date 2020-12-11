<template>
  <div class="container flex h-full">
    <line-chart 
      v-if="temploaded"
      :chartdata="tempdata"
      :options="options"
      />
      <line-chart
      v-if="pm25loaded"
      :chartdata="pm25data"
      :options="options"
      />
      <line-chart
      v-if="pm10loaded"
      :chartdata="pm10data"
      :options="options"
      />
  </div>
</template>

<script>
import LineChart from './Chart.vue'

export default {
  name: 'LineChartContainer',
  components: { LineChart },
  data: () => ({
    loaded: false,
    chartdata: null,
    options: {
      responsive: true,
      maintainAspectRatio: false
    },
    tempdata: null,
    temploaded: false,
    tempcolor: 'rgba(138,194,255,0.9)',
    tempbgcolor: 'rgba(138,194,255,0)',
    pm25loaded: false,
    pm25data: null,
    pm25color: 'rgba(160,135,199,0.9)',
    pm25bgcolor: 'rgba(160,135,199,0)',
    pm10loaded: false,
    pm10data: null,
    pm10color: 'rgba(0,240,186,0.9)',
    pm10bgcolor: 'rgba(160,135,199,0)',
    sensorId: [],
    boxName: null,
    boxId: null,
  }),
  async mounted () {
    this.loaded = false
    try {
      fetch('https://api.opensensemap.org//statistics/descriptive?boxid=5e253fd4ff64c1001a8deb27&columns=lat,lon,boxName,boxId,unit&download=false&format=json&from-date=2020-12-03T20:22:03.723Z&operation=arithmeticMean&phenomenon=Temperatur&to-date=2020-12-10T20:22:03.723Z&window=1h')
      .then(res => res.json()).then(data => {this.tempdata=this.parseData(data[0],this.tempbgcolor,this.tempcolor); console.log(this.tempdata); this.temploaded=true;});
      fetch('https://api.opensensemap.org//statistics/descriptive?boxid=5e253fd4ff64c1001a8deb27&columns=lat,lon,boxName,boxId,unit&download=false&format=json&from-date=2020-12-03T20:22:03.723Z&operation=arithmeticMean&phenomenon=PM2.5&to-date=2020-12-10T20:22:03.723Z&window=1h')
      .then(res => res.json()).then(data => {this.pm25data=this.parseData(data[0],this.pm25bgcolor,this.pm25color), console.log(this.pm25data); this.pm25loaded=true;});
      fetch('https://api.opensensemap.org//statistics/descriptive?boxid=5e253fd4ff64c1001a8deb27&columns=lat,lon,boxName,boxId,unit&download=false&format=json&from-date=2020-12-03T20:22:03.723Z&operation=arithmeticMean&phenomenon=PM10&to-date=2020-12-10T20:22:03.723Z&window=1h')
      .then(res => res.json()).then(data => {this.pm10data=this.parseData(data[0],this.pm10bgcolor,this.pm10color), console.log(this.pm10data); this.pm10loaded=true;});
      
    //   const { userlist } = await fetch('/api/userlist')
    //   this.chartdata = userlist
    //   this.loaded = true
    } catch (e) {
      console.error(e)
    }
  },
  methods: {
      parseData: function (raw,bgcolor,chartcolor) {
        var data = [];
        var label = [];
        var sensorId = raw["sensorId"];
        this.sensorId.push(sensorId);
        this.boxName = raw["boxName"];
        this.boxId = raw["boxId"];
        var title = null;
        if (sensorId == "5e253fd4ff64c1001a8deb2a") {
            title = "Temperature";
        } else if (sensorId == "5e253fd4ff64c1001a8deb2b") {
            title = "PM 2.5"
        } else if (sensorId == "5e253fd4ff64c1001a8deb2c") {
            title = "PM 10"
        }

        for (var key of Object.keys(raw)) {
            if (key != "sensorId" && key != "lat" && key != "lon" && key !="boxName" && key!="boxId" && key!="unit") {
                data.push(raw[key]);
                label.push(key);
            }
        }

        var cdata = {
            labels: label,
            datasets: [{
                label: title,
                data: data,
                backgroundColor: bgcolor,
                borderColor: chartcolor

            }]
        };
        return cdata;
      }
  }
}
</script>