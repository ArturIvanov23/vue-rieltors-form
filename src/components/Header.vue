<template>
  <div>

    <v-navigation-drawer v-model="drawer" app clipped class="hidden-md-and-up">
      <v-list dense>
        <v-list-item>
          <v-list-item-content>
            <v-list-item-title>
              <v-dialog v-model="dialog" max-width="600px">
                <template v-slot:activator="{ on, attrs }">
                  <v-btn block v-bind="attrs" v-on="on">Новый риэлтор</v-btn>
                  <v-btn block v-on:click="visible=!visible; drawer=!drawer">Список риэлторов</v-btn>
                </template>
              </v-dialog>
            </v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar app clipped-left dense>
      <v-app-bar-nav-icon class="hidden-md-and-up" @click.stop="drawer = !drawer">
      </v-app-bar-nav-icon>
      <v-toolbar-items class="hidden-sm-and-down">
        <v-dialog v-model="dialog" max-width="650px">
          <template v-slot:activator="{ on, attrs }">
            <v-btn text small v-bind="attrs" v-on="on">Новый риэлтор</v-btn>
            <v-btn text small v-on:click="main=!main">Список риэлторов</v-btn>
          </template>
        </v-dialog>
      </v-toolbar-items>
      <v-spacer></v-spacer>
      <v-row align="center" style="max-width: 650px">
        <v-text-field
          :append-icon-cb="() => {}"
          placeholder="Поиск..."
          single-line
          append-icon="mdi-magnify"
          color="white"
          hide-details>
        </v-text-field>
      </v-row>
    </v-app-bar>
    <div>
      <MainForm v-if="main"/>
    </div>
  </div>
</template>

<script>
import MainForm from '@/components/MainForm'
export default {
  name: 'Header',
  components: {
    MainForm
  },
  data: () => ({
    main: false,
    drawer: false,
    dialog: false
  })
}
</script>

<style scoped>

</style>
