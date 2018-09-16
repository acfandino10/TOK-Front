<template>
    <div>
        <div style="padding:5%;">
            <h1 >¿Quieres conseguir más puntos?</h1><br/>
            <div> Tenemos muchas opciones para ti !</div>
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
                                    <div>
                                        <h3 class="headline mb-0">
                                            <div class="cust-font-fam" v-if="reward.name.length<8">{{ reward.name }}</div>
                                            <div class="cust-font-fam" v-if="reward.name.length>=8">{{ reward.name.substring(0,8)+".." }}</div>
                                        </h3>
                                        <div>
                                            <div class="cust-font-fam grey--text"><h3>Gana 450 puntos</h3></div>
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
      size: 'md',
      items: [
        { text: 'Extra small (2px)', value: 'xs' },
        { text: 'Small (4px)', value: 'sm' },
        { text: 'Medium (8px)', value: 'md' },
        { text: 'Large (16px)', value: 'lg' },
        { text: 'Extra large (24px)', value: 'xl' }
      ],
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
    @import url('https://fonts.googleapis.com/css?family=Amatic+SC|Cinzel|Pacifico|Sacramento|VT323');

    .cust-font-fam{
        font-family: 'Roboto', sans-serif !important;
        text-align: center;
    }
    .texttitle {
        font-family: 'VT323';
    }

</style>
