<template>
    <div>
        <v-row>
            <v-col cols="12">
                <div class="d-flex flex-column justify-center align-center">
                    <h3>Current Price of 1 BTC</h3>
                    <div v-for="cur in data.bpi" :key="cur">
                        <span>
                            {{ cur.code }}
                        </span>
                        <span>
                            {{ cur.rate_float }}
                        </span>


                    </div>

                </div>

            </v-col>
        </v-row>
        <v-row no-gutters class="pa-2">
            <v-col v-for="img in imgs" :key="img" cols="12" lg="4" md="6" sm="12">
                <v-card class="pa-2" outlined tile>
                    <img :src="img.src" alt="" srcset="" style="width: 100%;">
                </v-card>
            </v-col>
        </v-row>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    data() {
        return {
            data: null,
            loading: false,
            imgs: [
                { src: 'https://picsum.photos/id/1/200/300' },
                { src: 'https://picsum.photos/id/1/200/300' },
                { src: 'https://picsum.photos/id/1/200/300' }
            ]
        }
    },
    methods: {
        fetchData() {
            this.loading = true
            axios.get('https://api.coindesk.com/v1/bpi/currentprice.json')
                .then(response => {
                    console.log(response.data, 'fasdfds')
                    this.data = response.data;

                    this.loading = false
                })
                .catch(error => {
                    console.log(error)
                    this.data = null;

                });
        }
    },
    mounted() {
        this.fetchData()
    }



}
</script>

<style></style>