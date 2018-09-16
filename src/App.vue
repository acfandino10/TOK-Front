<template>
    <div id="app" style="padding-top:0px; margin-top:0px;">
        <div>
                <v-tabs style="padding:0px;"
                        v-model="active"
                        color="#DF0E20"
                        dark
                        slider-color="white">
                    <img class="fiximage" src="./assets/colpatrialogo.jpg"/>
                    <v-tab ripple>
                        <v-icon>card_giftcard</v-icon>
                    </v-tab>
                    <v-tab>
                    <v-icon>shopping_basket</v-icon>
                    </v-tab>
                    <v-tab ripple>
                        <v-icon>person</v-icon>
                    </v-tab>
                    <v-tab-item>
                        <v-card flat>
                            <Rewards/>
                        </v-card>
                    </v-tab-item>
                    <v-tab-item>
                        <v-card flat>
                            <img alt="Vue logo" src="./assets/logo.png">
                        </v-card>
                    </v-tab-item>
                </v-tabs>
        </div>
        <div class="mainFooter">
            <div>
                <a href="https://www.colpatria.com/">
                    <img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAJcEhZcwAADsMAAA7DAcdvqGQAAAK8SURBVGhD7ZnNi41RHMfvNCgvhWxtFJIiC6wUM6SpSTY2UjYkhQ1LqYmFouRlMUXDzHqykpUF5R+Qd9mRNImykbzc6/O750uu+7yc+9zncEznU9/O85zz/f7u79edO7d7byORSCRmF61WaweabDabd/6RbqBhtVMNCpxmiFgYU1u9wRDbVSAa6GlI7flDaEr5aKCn62rPH0J3lY8G60nt+UPovvLRYD2pPX/SIAGJbhBqz6AX6KO2vAgyCOffdekNmVtovR7C3mwHuR9BT3T+GY2jt3b/J+wHGeQsuqLbUvBeZBlQ+Q7YX8L5LtZFrAfMnwVnQQbZyDLAetnt5IPnIcugSueCbw+6ia65ZCfsBxlkhazmPYo+6agLzg7LWgr2Nfg/uGQn7AcZZKusbbhfiaZR12uHvc2yFYJ1A953LtUNZ0EGGZe1A/ZXozPoAfom+xYdF4L/pPyZcB5kkC9ok+yZcL4QrUXLtFUIPvuHkAvnQQY5gs5zuVSRvqHetKueTahBRmWtDWo+VvlMQg1yW9ZaoN5ylc4lyCAGnhOy9w3lDrmq+QQbxMA3gVYpVgnK2BvrI1cxn2CD4PmK9qOd3Ja+c+dBfrerWIz1pIg/FlK+EHxTilSCEguo8cxVKyboIAbeCyzzFO0JslddlXKCD2Lgf4lOoXUqUQreg4p7YT0p6o+FlPcC/2t0jMs5KlEI3uOo6dJ+YK93EM6s6adc3mO9hEa59h1gPvL+HPM75GofxP6M9nE5V/ZS8Nqnwb2WbRepgPWkcv5YSPlc8LxB59AIt4sV/YXtcTaM7NPkq3aoD6gR/jVikHmPniN7xma0XRvWk9rzx0LKR0MaRPloqDrI7PgSm9yki8cDg0yoPX8IDSkfE9vUXm8QHHP5KKj209tP7JmxpxRl/VD5N2SP3fEdWiKRSPzvNBo/AEFtHBwULZrpAAAAAElFTkSuQmCC">
                </a>
                <a href="https://www.colpatria.com/">
                    <img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAJcEhZcwAADsMAAA7DAcdvqGQAAANdSURBVGhD7Zk9axRRFIYDimg+NEKMWFoINoK91mIlQgyigVTaSAR/QMTGxDT6CyyEFdEkWqQTEZIIJpIQUwl2oqBRET86CW58zs4ruHHvfNx7Z2KxDxzu7Mx73nPOZjIzu9vRpk2b6qjX6/0bGxuDrGPEFDHH62XFrPbZsTNEv9L+D2iwl6ZGiCWizutcmBYWiRFe9squeqw4MUEjP6yxEPD4ToyxWe1AFB0mPiVtxAPPNWJIZcqDIj3EXdUtDdXoVtm4YL6fWElKVcKy1VT5OGC4j3itApVhNa222ggDIzudVuVdOdReYgk/zTC6l1huHfRQUzt+YDAsry2HXvyuZuTuJTnqJRa/L4Td2Y/xss/qsG2n7gHiEHE2Uf4Lx9ZYit9nSJpoOESCRmZY9si+JWiOJOrWcHxc0nyQY48dwXfsP+D1lGWb7J1kDQLfiPx/FQzt+ScKeK0TB2WdSo5BzO+S5NkgfqG8YPB6KNtMcg6yIHk6CPuJ3E+xWWA1Iusm2N9FjBL2aP9EsaA0J2h+sTQuFKkgGmxkRILCJ2XdBPtrkhSG3AHZuEE0Ln0sjsu6Ceq80/HCkHtdNm7QTSbyaLQchP12BfKCQe7Lxg2ieeljEX0QmJWNGwZ5KXEsyviLrMjGTcgg5C6y2Kn5dxyWdRPsv7NJN6n8TNCtysYNomfSF4bc87LxgvzLskoF3bxS3CCakr4wEQa5KatU0D1QihtE9m2GFxEGeSSrVNBlX34RDUhfmAiD5Pokiq7lTbYJdH0IvR5RQgfBIvNKRo2fRJdS0kH4XHmFIM/7qkXuNGsm6OZkkQ3iaI/xEPU+Qm8XZZENevtg9TVJDSbaIPT0nmWnLPJB0o0kPZiYg4wqPT8k7SY+yCOEKIPQy1uW1M/8Tkg+l9gEETwIfRgnlOoHBt4fgESMQW4rzR98OjHK9TDnIGgQats3MJ1KCwMz+xL7VWJdGO9B9Ab6/V+4wNDu+PaFclG8BqHWvL2BkscF413UsDtyEQoNQg3jFpvbJS0PCtmvsnkvzbkHwfMNy2lJqoGidp+5RuGscz1zEHw+E1fY3KHD1UPxbpq4wGq/o69bY5toOQjaj8QMMYSmnN8LfaEh+yniFHGVqBGP2XdUh5vgWI8227RpUzodHb8BF4l2VWFfArAAAAAASUVORK5CYII=">
                </a>
            </div><br/>
            <i style="font-size:1em;">Desarrollo enfocado en solución a uno de los casos presentados por The Only Key 2018 la Hackaton de Scotiabank Colpatria</i>
            <br/>
            <hr class="line"/>
            &copy;2018 — <strong>Scotiabank Hackaton</strong>
        </div>
    </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import Rewards from './components/Rewards.vue'

export default {
  name: 'app',
  components: {
    HelloWorld,
    Rewards
  },
  data: () => ({
    icons: [
      'fab fa-facebook',
      'fab fa-twitter',
      'fab fa-google-plus',
      'fab fa-linkedin',
      'fab fa-instagram'
    ],
    active: null
  }),
  methods: {
  }
}
</script>

<style>
    #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }
    .mainFooter {
        color: white;
        margin-top:10%;
        padding-top:5%;
        padding-bottom:2%;
        background-color: gray;
    }
    .line {
        display: block;
        height: 1px;
        border: 0;
        border-top: 1px solid #ccc;
        margin: 1em 0;
        padding: 0;
    }
    .fiximage {
        height: 50px;
        width: auto;
    }

</style>
