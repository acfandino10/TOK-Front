<template>
    <div id="app" style="padding-top:0px; margin-top:0px;">
        <div class="toolsbar">
            <v-tabs style="padding:0px;"
                    v-model="active"
                    color="#DF0E20"
                    dark
                    slider-color="white">
                <img class="fiximage" src="https://acfandino10.github.io/TOKpages/img/colpatrialogo.34c5c477.jpg"/>
                <v-tab ripple>
                    <v-icon>card_giftcard</v-icon>
                </v-tab>
                <v-tab>
                    <v-icon>shopping_basket</v-icon>
                </v-tab>
                <v-tab-item>
                    <v-card flat>
                        <div>
                            <!--<v-tooltip v-if="notifyNow" fixed="true" abslute="true" top>
                                <span>{{notificationMessage}}</span>
                            </v-tooltip>
                            <v-btn v-on:click="notifyExample()">Prueba Notificar</v-btn>-->
                            <div class="barra">
                                <div class="points"> Tienes <b>{{client.points}}</b> puntos.</div>
                                <v-btn class="staticsize" round color="#DF0E20" style="color:white;">
                                    <v-progress-linear color="white" v-model="valueDeterminate"></v-progress-linear>
                                </v-btn>
                            </div>
                            <div class="tags" v-if="showTags" style="padding:5%;">
                                <v-btn v-for="tag in tags" :key="tag" class="tag" small color="white"
                                       style="color:#DF0E20;border: 0.8px solid #DF0E20 !important; font-weight: bold"
                                       @click="selectedTags.push(tag)">{{tag}}
                                </v-btn>
                                <v-btn v-on:click="toggleTags()" color="#DF0E20" style="color:white;font-weight: bold">
                                    Ok!
                                </v-btn>
                            </div>
                            <v-flex xs12>
                                <v-card>
                                    <v-container v-bind="{ [`grid-list-${size}`]: true }" fluid>
                                        <v-layout row wrap>
                                            <v-flex v-for="(reward, index) in rewards" :key="reward.id" xs6>
                                                <v-card class="smallersize" min-height="270px">
                                                    <img style="padding-top:10%;" v-bind:src="reward.photoUrl"
                                                         height="130px"/>
                                                    <v-card-title primary-title
                                                                  style="padding-top:2%; padding-bottom:2%;">
                                                        <div></div>
                                                        <div style="child-align: middle">
                                                            <h3 class="headline mb-0">
                                                                <div class="cust-font-fam" v-if="reward.name.length<12">
                                                                    {{ reward.name }}
                                                                </div>
                                                                <div class="cust-font-fam"
                                                                     v-if="reward.name.length>=12">{{
                                                                    reward.name.substring(0,12)+'..' }}
                                                                </div>
                                                            </h3>
                                                            <div>
                                                                <div slot="activator"
                                                                     style="horiz-align: left; padding-left:3%;">
                                                                    {{reward.pointsCost}} Pts
                                                                    <v-icon @click="toggleView(index)">arrow_drop_down
                                                                    </v-icon>
                                                                    <v-btn v-if="client.points >= reward.pointsCost"
                                                                           round color="green" style="color:white;"
                                                                           @click="comprar(reward)">
                                                                        Comprar
                                                                    </v-btn>
                                                                    <div v-else round color="green"
                                                                         style="color:white;">
                                                                        <v-btn fab small color="green"
                                                                               style="color:white;">
                                                                            <v-icon>credit_card</v-icon>
                                                                        </v-btn>
                                                                        <v-btn v-on:click="buyWithFriends(reward)" fab small
                                                                               color="#DF0E20" style="color:white;">
                                                                            <v-icon>people</v-icon>
                                                                        </v-btn>
                                                                    </div>
                                                                </div>
                                                                <div v-show="false" class="cust-font-fam grey--text">
                                                                    <h3>Te faltan 450 puntos</h3></div>
                                                            </div>
                                                        </div>
                                                    </v-card-title>
                                                    <v-slide-y-transition>
                                                        <v-card-text v-show="reward.toggle">
                                                            {{reward.description}}
                                                        </v-card-text>
                                                    </v-slide-y-transition>
                                                </v-card>
                                            </v-flex>
                                        </v-layout>
                                    </v-container>
                                </v-card>
                            </v-flex>
                        </div>
                    </v-card>
                </v-tab-item>
                <!--<v-tab-item>-->
                <!--<v-card flat>-->
                <!--<div>-->
                <!--<div style="padding:5%;">-->
                <!--<h1>¿Quieres conseguir más puntos?</h1><br/>-->
                <!--<div> Tenemos muchas opciones para ti !</div>-->
                <!--</div>-->
                <!--<v-flex xs12>-->
                <!--<v-card>-->
                <!--<v-container v-bind="{ [`grid-list-${size}`]: true }" fluid>-->
                <!--<v-layout row wrap>-->
                <!--<v-flex v-for="n in 9" :key="n" xs6>-->
                <!--<v-card class="smallersize">-->
                <!--<v-img :src="`https://unsplash.it/150/300?image=${Math.floor(Math.random() * 100) + 1}`"-->
                <!--height="130px">-->
                <!--</v-img>-->
                <!--<v-card-title primary-title-->
                <!--style="padding-top:2%; padding-bottom:2%;">-->
                <!--<div></div>-->
                <!--<div>-->
                <!--<h3 class="headline mb-0">-->
                <!--<div class="cust-font-fam" v-if="reward.name.length<8">-->
                <!--{{ reward.name }}-->
                <!--</div>-->
                <!--<div class="cust-font-fam" v-if="reward.name.length>=8">-->
                <!--{{ reward.name.substring(0,8)+'..' }}-->
                <!--</div>-->
                <!--</h3>-->
                <!--<div>-->
                <!--<div class="cust-font-fam grey&#45;&#45;text"><h3>Gana 450-->
                <!--puntos</h3></div>-->
                <!--</div>-->
                <!--</div>-->
                <!--</v-card-title>-->
                <!--<v-slide-y-transition>-->
                <!--<v-card-text v-show="show">-->
                <!--{{reward.description}}-->
                <!--</v-card-text>-->
                <!--</v-slide-y-transition>-->
                <!--</v-card>-->
                <!--</v-flex>-->
                <!--</v-layout>-->
                <!--</v-container>-->
                <!--</v-card>-->
                <!--</v-flex>-->
                <!--</div>-->
                <!--</v-card>-->
                <!--</v-tab-item>-->
                <div right class="intro" style="margin-left:13%;"><span> ¡ Hola, {{client.firstName}} !</span></div>
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
            </div>
            <br/>
            <i style="font-size:1em;">Desarrollo enfocado en solución a uno de los casos presentados por The Only Key
                2018 la Hackaton de Scotiabank Colpatria</i>
            <br/>
            <hr class="line"/>
            &copy;2018 — <strong>Scotiabank Hackaton</strong>
        </div>
    </div>
</template>

<script>
  import swal from 'sweetalert'

  export default {
    name: 'app',
    components: {},
    data: () => ({
      client: {
        points: 0
      },
      rewardss: [],
      icons: [
        'fab fa-facebook',
        'fab fa-twitter',
        'fab fa-google-plus',
        'fab fa-linkedin',
        'fab fa-instagram'
      ],
      active: null,
      showTags: true,
      notifyNow: false,
      indexSelected: -1,
      notificationMessage: 'Haz comprado no se que cosas con éxito !',
      valueDeterminate: 60,
      indexSelected: '1',
      size: 'md',
      items: [
        {text: 'Extra small (2px)', value: 'xs'},
        {text: 'Small (4px)', value: 'sm'},
        {text: 'Medium (8px)', value: 'md'},
        {text: 'Large (16px)', value: 'lg'},
        {text: 'Extra large (24px)', value: 'xl'}
      ],
      tags: [
        'Accesorios para hombre y mujer', 'Cuidado personal', 'Deportes', 'Hogar', 'Juguetería', 'Tecnología',
        'Bonos de establecimientos', 'Entradas a cine', 'Cenas', 'Excursiones y experiencias turísticas',
        'Millas Lifemiles', 'Millas Latampass', 'Celulares'
      ],
      show: false,
      selectedTags: []
    }),
    async mounted () {
      const param = window.location.search.replace('?', '').split('&').map(v => v.split('=')).map(v => ({[v[0]]: v[1]}))[0]
      this.client = await fetch(`https://hackathon.inal.co/clients/${param.cedula}`).then(res => res.json())
      this.rewardss = (await fetch(`https://hackathon.inal.co/rewards`).then(res => res.json())).map(r => {
        r.toggle = false
        return r
      })
    },
    computed: {
      rewards () {
        if (this.selectedTags.length > 0) return this.rewardss.filter(r => this.selectedTags.includes(r.category))
        else return this.rewardss
      }
    },
    methods: {
      comprar () {
        swal({
          title: '',
          text: 'Ingresa el número de tu amigo !',
          content: 'input',
          dangerMode: true,
          icon: 'success',
          button: {
            text: 'Ok!',
            closeModal: false,
          },
        })
      },
      buyWithFriends (reward) {
        swal({
          text: 'Ingresa el número de tu amigo!',
          content: 'input',
          dangerMode: true,
          icon: 'success',
          button: {
            text: 'Ok!',
            closeModal: false,
          },
        }).then(number => {
          if (!number) return
          swal.close()
          fetch('https://nplat.inal.co/messages/text', {
            headers: {
              'Accept': 'application/json',
              'Content-Type': 'application/json'
            },
            body: JSON.stringify({
              text: `${this.client.firstName} te esta pidiendo ${reward.pointsCost - this.client.points} puntos para comprar ${reward.name}. Responde SI para aceptar`,
              telephone: number,
              allChannels: true,
              fbMessengerTag: 'NON_PROMOTIONAL_SUBSCRIPTION'
            }),
            method: 'POST'
          })
        })
      },
      toggleTags () {
        if (this.showTags) this.showTags = false
        else this.showTags = true
      },
      toggleView (index) {
        if (this.rewards[index].toggle) this.rewards[index].toggle = false
        else this.rewards[index].toggle = true
      },
      setRewardIndex: function (index) {
        this.indexSelected = index
        if (this.show) this.show = false
        else this.show = true
      },
      notifyExample () {
        this.notifyNow = true
      }
    }
  }
</script>

<style>
    @import url('https://fonts.googleapis.com/css?family=Kaushan+Script|Crete+Round|VT323');
    @import url('https://fonts.googleapis.com/css?family=Amatic+SC|Cinzel|Pacifico|Sacramento|VT323');

    .cust-font-fam {
        font-family: 'Roboto', sans-serif !important;
        text-align: center;
    }

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
        margin-top: 10%;
        padding-top: 5%;
        padding-bottom: 2%;
        padding-left: 5%;
        padding-right: 5%;
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

    .intro {
        font-family: 'Kaushan Script';
        font-size: 1.5em;
        color: white;
        display: inline-block;
        margin: 0;
        padding: 0;
        text-align: center;

    }

    .cust-font-fam {
        font-family: 'Roboto', sans-serif !important;
        text-align: center;
    }

    .staticsize {
        width: 70%;
    }

    .points {
        font-family: 'VT323';
        padding: 5%;
        font-size: 3em;
    }

</style>
