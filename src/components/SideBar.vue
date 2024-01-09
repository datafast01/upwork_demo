<template>
    <div>
        <v-navigation-drawer v-model="drawer" dark expand :clipped="$vuetify.breakpoint.lgAndUp" app>
            <v-list dense>
                <template v-for="item in itemsDrawer">
                    <v-list-group v-if="item.children" :key="item.text" v-model="item.model" :prepend-icon="item.icon">
                        <template v-slot:activator>
                            <v-list-item-content>
                                <v-list-item-title>
                                    {{ item.text }}
                                </v-list-item-title>
                            </v-list-item-content>
                        </template>
                        <v-list-item v-for="(child, i) in item.children" :key="i" link :to="child.link">
                            <v-list-item-icon v-if="child.icon">
                                <v-icon>{{ child.icon }}</v-icon>
                            </v-list-item-icon>
                            <v-list-item-content>
                                <v-list-item-title>
                                    {{ child.text }}
                                </v-list-item-title>
                            </v-list-item-content>
                        </v-list-item>
                    </v-list-group>
                    <v-list-item v-else :key="item.text" link :to="item.link">
                        <v-list-item-icon>
                            <v-icon>{{ item.icon }}</v-icon>
                        </v-list-item-icon>
                        <v-list-item-content>
                            <v-list-item-title>
                                {{ item.text }}
                            </v-list-item-title>
                        </v-list-item-content>
                    </v-list-item>
                </template>
            </v-list>
        </v-navigation-drawer>

        <v-app-bar :clipped-left="$vuetify.breakpoint.lgAndUp" app color="blue" dark class="top-bar">

            <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
            <span v-if="name">
                {{ name }}
            </span>
            <v-btn depressed :loading="loading" @click="login" v-else>
                Login
            </v-btn>


        </v-app-bar>
    </div>
</template>
<script>
import axios from 'axios'
export default {
    data() {
        return {
            drawer: true,
            itemsDrawer: [{
                icon: 'mdi-security',
                text: 'Menu 1',
            },
            {
                icon: 'mdi-text-box-multiple-outline',
                text: 'Menu 2',
            },
            {
                icon: 'mdi-contacts',
                text: 'Menu 3',
                model: false,

            }
            ],
            data: null,

            name: null,
            loading: false
        }
    },

    methods: {
        login() {
            this.loading = true
            axios.get('https://randomuser.me/api/')
                .then(response => {
                    console.log(response.data, 'fasdfds')
                    this.data = response.data;
                    this.name = this.data.results[0].name.title + ' ' + this.data.results[0].name.first + ' ' + this.data.results[0].name.last
                    console.log(this.name)
                    this.loading = false
                })
                .catch(error => {
                    console.log(error)
                    this.data = null;

                });
        }
    }


}
</script>

<style scoped>
::v-deep .v-toolbar__content {

    justify-content: space-between !important;
    margin-right: 10px;
    margin-left: 10px;
}
</style>