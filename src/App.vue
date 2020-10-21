<template>
  <div id="app">
    <h1>Wi-Fi to QRcode</h1>

    <div>
      <input type="text" v-model="wifi.ssid" placeholder="SSID">
    </div>

    <div>
      <input type="text" v-model="wifi.pass" placeholder="PASSWORD">
    </div>

    <div>
      <select v-model="wifi.type">
        <option value="WEP">WEP</option>
        <option value="WPA">WPA/WPA2</option>
      </select>
    </div>

    <button @click="generate">作成</button>

    <div>
      <vue-qrcode v-if="qrcode.targetText" :type="qrcode.type" :value="qrcode.targetText" :options="qrcode.option" tag="img"></vue-qrcode>
    </div>
  </div>
</template>

<script>
    import VueQrcode from "@chenfengyuan/vue-qrcode";

    export default {
        name: 'App',
        components: {
            VueQrcode,
        },
    data(){
        return{
            wifi:{
                ssid: "",
                pass: "",
                type: "WPA",
            },
            qrcode:{
                targetText: "",
                option: {
                    errorCorrectionLevel: "M",
                    maskPattern: 0,
                    margin: 5,
                    scale: 2,
                    width: 150,
                    color: {
                        dark: "#000000FF",
                        light: "#FFFFFFFF"
                    }
                }
            }
        }
    },
        methods:{
            generate(){ // QRコードを生成
                if( this.wifi.ssid !== "" ){
                    if( this.wifi.pass === "" ){
                        this.qrcode.targetText =
                            "WIFI:T:" + this.wifi.type +
                            ";S:" + this.wifi.ssid + ";;";
                    }else{
                        this.qrcode.targetText =
                            "WIFI:T:" + this.wifi.type +
                            ";S:" + this.wifi.ssid +
                            ";P:" + this.wifi.pass + ";;";
                    }

                }
            }
        }
    }
</script>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
  input[type="text"], select{
    margin-bottom: 10px;
  }
</style>
