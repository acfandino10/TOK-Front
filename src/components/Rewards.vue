<template>
    <div>
        <!--<v-tooltip v-if="notifyNow" fixed="true" abslute="true" top>
            <span>{{notificationMessage}}</span>
        </v-tooltip>
        <v-btn v-on:click="notifyExample()">Prueba Notificar</v-btn>-->
        <div class="barra">
            <div class="points"> Tienes <b>{{$parent.client.points}}</b> puntos.</div>
            <v-btn class="staticsize" round color="#DF0E20" style="color:white;">
                <v-progress-linear color="white" v-model="valueDeterminate"></v-progress-linear>
            </v-btn>
        </div>
        <div class="tags" v-if="showTags" style="padding:5%;">
            <v-btn v-for="tag in tags" :key="tag" class="tag" small color="white" style="color:#DF0E20;border: 0.8px solid #DF0E20 !important; font-weight: bold" @click="changeRewardsArray(tag)">{{tag}}</v-btn>
            <v-btn v-on:click="toggleTags()" color="#DF0E20" style="color:white;font-weight: bold">Ok!</v-btn>
        </div>
        <v-flex xs12>
            <v-card>
            <v-container v-bind="{ [`grid-list-${size}`]: true }" fluid>
              <v-layout row wrap>
                <v-flex v-for="(reward, index) in rewardArray" :key="reward.id" xs6>
                  <v-card class="smallersize" min-height="270px">
                    <img style="padding-top:10%;" v-bind:src="reward.photoUrl"  height="130px"/>
                      <v-card-title primary-title style="padding-top:2%; padding-bottom:2%;">
                          <div></div>
                          <div style="child-align: middle">
                              <h3 class="headline mb-0">
                                  <div class="cust-font-fam" v-if="reward.name.length<12">{{ reward.name }}</div>
                                  <div class="cust-font-fam" v-if="reward.name.length>=12">{{ reward.name.substring(0,12)+".." }}</div>
                              </h3>
                              <div>
                                  <div slot="activator" style="horiz-align: left; padding-left:3%;">
                                      {{reward.pointsCost}} Pts
                                      <v-icon @click="toggleView(index)">arrow_drop_down</v-icon>
                                      <v-btn v-if="mockup.client.points>=reward.pointsCost" round color="green" style="color:white;">
                                          Comprar
                                      </v-btn>
                                      <div v-else round color="green" style="color:white;">
                                          <v-btn fab small color="green" style="color:white;">
                                              <v-icon>credit_card</v-icon>
                                          </v-btn>
                                          <v-btn v-on:click="buyWithFriends()" fab small color="#DF0E20" style="color:white;">
                                              <v-icon>people</v-icon>
                                          </v-btn>
                                      </div>
                                  </div>
                                  <div v-show="false" class="cust-font-fam grey--text"><h3>Te faltan 450 puntos</h3></div>
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
</template>
<script>
  import swal from 'sweetalert'

  export default {
    data: () => ({
      showTags: true,
      notifyNow:false,
      indexSelected: -1,
      notificationMessage: "Haz comprado no se que cosas con éxito !",
      valueDeterminate:50,
      rewardArrayW: '',
      indexSelected:'1',
      size: 'md',
      items: [
        { text: 'Extra small (2px)', value: 'xs' },
        { text: 'Small (4px)', value: 'sm' },
        { text: 'Medium (8px)', value: 'md' },
        { text: 'Large (16px)', value: 'lg' },
        { text: 'Extra large (24px)', value: 'xl' }
      ],
      tags: [
        "Accesorios", "Cuidado personal", "Deportes", "Hogar", "Juguetería", "Tecnología", "Bonos", "Cine", "Cenas", "Actividades", "Turismo", "Millas", "Celulares"
      ],
      /*tiposBonos:
        [
          "Bonos Establecimientos", "Entradas a cine", "Cenas", "Turismo", "Millas Lifemiles", "Milla Latam Miles", "Reposición Celulares Claro"
        ],*/
      reward: {
          name: 'Recompensa Recompensa Recompensa Recompensa',
          points: '1000',
          description: 'Descripcion Descripcion Descripcion Descripcion',
      },
      mockup: {
          client: {
              firstName: 'Ana',
              lastName: 'Fandino',
              document: '10128392383',
              birthday: '1996-01-01',
              email: 'anafandino@gmail.com',
              telephone: '12345678',
              address: 'calle falsa 123',
              points: 1800,
              rewards: [
                  {
                    id: 1,
                    toggle:false,
                    name: 'Collar Cuero Plateado',
                    description: 'Cadenita en plata italiana y tres esferitas cuarzo rosa Marca: Scarlett Color Disponible: Rosa Material de Fabricación: Plata italiana y cuarzo Fabricado en: Colombia.',
                    category: 'Accesorios para hombre y mujer',
                    pointsCost: 1800,
                    moneyCost: 78000,
                    photoUrl: 'https://www.catalogodavipuntos.com/1611-tm_home_default/collar-cuero-plateado.jpg',
                    withFriends: false
                  },
                  {
                    id: 2,
                    toggle:false,
                    name: 'Kit de Afeitar Set The Mens Soap Alpha',
                    description: 'Máximo control para un estilo perfecto de la barba, del cabello y del pelo corporal.',
                    category: 'Cuidado personal',
                    pointsCost: 2000,
                    moneyCost: 10000,
                    photoUrl: 'https://www.catalogodavipuntos.com/2056-tm_thickbox_default/juego-de-afeitar-set-the-men-s-soap-alpha.jpg',
                    withFriends: false
                  },
                  {
                    id: 3,
                    toggle:false,
                    name: 'Plancha a Vapor I-Pro 200 Babyliss',
                    description: 'Plancha a vapor con  placas de ceramica practicas y rápidas para alisar todo tipo de cabello ',
                    category: 'Cuidado personal',
                    pointsCost: 1559,
                    moneyCost: 82000,
                    photoUrl: 'https://www.catalogodavipuntos.com/1673-tm_thickbox_default/plancha-a-vapor-i-pro-200-babyliss.jpg',
                    withFriends: false
                  },
                  {
                    id: 4,
                    toggle:false,
                    name: 'Kit  Verbane  cremas hidrantantes y aceite corporale',
                    description: 'Kit de cremas 2 hidratantes y un aceite corporal aromatizante',
                    category: 'Cuidado personal',
                    pointsCost: 2300,
                    moneyCost: 64200,
                    photoUrl: 'https://www.catalogodavipuntos.com/1660-tm_thickbox_default/kit-pequeno-de-2-cremas-hidratantes-aceite-corporal-.jpg',
                    withFriends: false
                  },
                  {
                    id: 5,
                    toggle:false,
                    name: 'Patineta Scooter Mini de Micro Roja',
                    description: 'la patineta para niños más segura y famosa del mundo, la patineta mini micro',
                    category: 'Juguetería',
                    pointsCost: 3400,
                    moneyCost: 73000,
                    photoUrl: 'https://www.catalogodavipuntos.com/1457-tm_thickbox_default/patineta-scooter-mini-de-micro-roja.jpg',
                    withFriends: false
                  },
                  {
                    id: 6,
                    toggle:false,
                    name: 'Bose - Audífonos Quiet Control 30 - Negros',
                    description: 'on los audífonos QuietControl 30 podemos decidir que tanto queremos escuchar de ello. Ahora podemos variar el nivel de cancelación de ruido que nos acomode más logrando un balance entre el audio y volumen de tal forma que no moleste en absoluto al oído.',
                    category: 'Tecnología',
                    pointsCost: 5000,
                    moneyCost: 200000,
                    photoUrl: 'https://pisces.bbystatic.com/image2/BestBuy_MX/images/products/1000/1000203321_ra.jpg',
                    withFriends: false
                  },
                  {
                    id: 7,
                    toggle:false,
                    name: 'Peluche Oso de Kisses Camel',
                    description: 'Una gran compañía suave y esponjosa puede ser tu gran amigo. Son peluches de gran calidad y muy tiernos. ¡Anímate a comprarlo!',
                    category: 'Juguetería',
                    pointsCost: 800,
                    moneyCost: 42000,
                    photoUrl: 'https://www.catalogodavipuntos.com/1440-tm_thickbox_default/peluche-oso-de-kisses-camel.jpg',
                    withFriends: false
                  }
              ]
          }
      },
      rewardArray: [],
      show: false
    }),
    mounted:
        function(){
            this.rewardArray = this.mockup.client.rewards
            return this.rewardArray
        },
    methods: {
      buyWithFriends () {
        swal({
          text: 'Ingresa el número de tu amigo !',
          content: 'input',
          dangerMode: true,
          icon: 'success',
          button: {
            text: 'Ok!',
            closeModal: false,
          },
        }).then(number => {
          if (!number) throw null
          swal.close()
        })
      },
      toggleTags () {
        if (this.showTags) this.showTags = false
        else this.showTags = true
      },
      toggleView (index) {
        if (this.rewardArray[index].toggle) this.rewardArray[index].toggle = false
        else this.rewardArray[index].toggle = true
      },
      setRewardIndex: function (index) {
        this.indexSelected = index
        if (this.show) this.show = false
        else this.show = true
      },
      notifyExample () {
        this.notifyNow = true
      },
      changeRewardsArray: function (tagName) {
        this.rewardArray = this.mockup.client.rewards

        function isTag (tag) {
          return tag.category === tagName
        }

        var auxArray = this.rewardArray.filter(isTag)
        this.rewardArray = auxArray

      }
    }
  }
</script>
<style scoped>
    @import url('https://fonts.googleapis.com/css?family=Kaushan+Script|Crete+Round|VT323');

    .cust-font-fam{
        font-family: 'Roboto', sans-serif !important;
        text-align: center;
    }
    .staticsize{
        width: 70%;
    }
    .points{
        font-family: 'VT323';
        padding:5%;
        font-size:3em;
    }

</style>
