<template>
    <div>
        <div class="intro"> Hola, Juan</div>
        <div class="barra">
            <div class="staticsize points"> Tienes 9,000 puntos.</div>
            <v-btn class="staticsize" round color="#DF0E20" style="color:white;">
                <v-progress-linear color="white" v-model="valueDeterminate"></v-progress-linear>
            </v-btn>
        </div>
        <div class="tags" style="padding:5%;">
            <v-btn v-for="tag in tags" small="true" color="#DF0E20" style="color:white; font-weight: bold">{{tag}}</v-btn>
        </div>
        <v-flex xs12>
            <v-card>
            <v-container v-bind="{ [`grid-list-${size}`]: true }" fluid>
              <v-layout row wrap>
                <v-flex v-for="n in 9" :key="n" xs6>
                  <v-card class="smallersize">
                    <v-img :src="`https://unsplash.it/150/300?image=${Math.floor(Math.random() * 100) + 1}`" height="130px">
                    </v-img>
                      <v-card-title primary-title style="padding-top:2%; padding-bottom:2%;">
                          <div></div>
                          <div style="child-align: middle">
                              <h3 class="headline mb-0">
                                  <div class="cust-font-fam" v-if="reward.name.length<8">{{ reward.name }}</div>
                                  <div class="cust-font-fam" v-if="reward.name.length>=8">{{ reward.name.substring(0,8)+".." }}</div>
                              </h3>
                              <div>
                                  <div slot="activator" style="horiz-align: left; padding-left:3%;">
                                      300 Puntos
                                      <v-btn fab small @click="show = !show" color="#DF0E20" style="color:white;">
                                          <v-icon>vpn_key</v-icon>
                                      </v-btn>
                                  </div>

                                  <div v-show="false" class="cust-font-fam grey--text"><h3>Te faltan 450 puntos</h3></div>
                              </div>
                          </div>
                      </v-card-title>
                    <v-slide-y-transition>
                        <v-card-text v-show="show">
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
  export default {
    data: () => ({
      valueDeterminate:50,
      size: 'md',
      items: [
        { text: 'Extra small (2px)', value: 'xs' },
        { text: 'Small (4px)', value: 'sm' },
        { text: 'Medium (8px)', value: 'md' },
        { text: 'Large (16px)', value: 'lg' },
        { text: 'Extra large (24px)', value: 'xl' }
      ],
      tags: [
        "Accesorios", "Cuidado Personal", "Deportes", "Hogar", "Juguetería", "Tecnología", "Bonos", "Cine", "Cenas", "Actividades", "Turismo", "Millas", "Celulares"
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
      show: false
    })
  }
</script>
<style scoped>
    @import url('https://fonts.googleapis.com/css?family=Permanent+Marker|Crete+Round');

    .cust-font-fam{
        font-family: 'Roboto', sans-serif !important;
        text-align: center;
    }
    .intro{
        font-family: 'Permanent Marker';
        font-size: 4em;
        text-align: center;
        horiz-align: center;
        padding:5%;
    }
    .staticsize{
        width: 70%;
    }
    .points{
        font-family: 'Crete Round';
        padding:5%;
    }

</style>
