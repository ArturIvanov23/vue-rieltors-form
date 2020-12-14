<template>
  <div>

    <v-data-table :headers="headers" :items="rieltors" class="elevation-1">
      <template v-slot:top>
        <v-toolbar flat color="white">
          <v-spacer></v-spacer>
          <v-dialog v-model="dialog" max-width="700px">
            <v-card>
              <v-card-title>
                <span class="headline">{{ formTitle }}</span>
              </v-card-title>

              <v-card-text>
                <v-container id="dropdown">
                  <v-row>
                    <v-col cols="12" sm="6" md="4">
                      <v-text-field v-model="editedItem.ID" label="ID"></v-text-field>
                    </v-col>
                    <v-col cols="12" sm="6" md="4">
                      <v-text-field v-model="editedItem.GUID" label="GUID"></v-text-field>
                    </v-col>
                    <v-col cols="12" sm="6" md="4">
                      <v-text-field v-model="editedItem.name" label="Имя"></v-text-field>
                    </v-col>
                    <v-col cols="12" sm="6" md="4">
                      <v-text-field v-model="editedItem.surname" label="Фамилия"></v-text-field>
                    </v-col>
                    <v-col cols="12" sm="4" md="4">
                      <v-overflow-btn v-model="editedItem.dep" class="my-2" :items="dropdownDep" label="Подразделение" target="#dropdown">

                      </v-overflow-btn>
                    </v-col>
                    <v-col cols="12" sm="6" md="4">
                      <v-text-field v-model="editedItem.dateReg" label="Дата регистрации"></v-text-field>
                    </v-col>
                  </v-row>
                </v-container>
              </v-card-text>

              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn color="blue darken-1" text @click="close">Отмена</v-btn>
                <v-btn color="blue darken-1" text @click="save">Сохранить</v-btn>
                <v-btn color="blue darken-1" text @click="close(deleteItem(item))">
                  Удалить
                  <v-icon large>mdi-delete</v-icon>
                </v-btn>
              </v-card-actions>
            </v-card>
          </v-dialog>
        </v-toolbar>
      </template>
      <template v-slot:item.actions="{ item }">
        <v-icon small class="mr-2" @click="editItem(item)">
          mdi-pencil
        </v-icon>
      </template>
      <template v-slot:no-data>
        <v-btn color="primary" @click="initialize">Reset</v-btn>
      </template>
    </v-data-table>

  </div>
</template>

<script>
export default {
  name: 'MainForm',
  data: () => ({
    visible: false,
    drawer: false,
    dialog: false,
    headers: [
      {
        text: 'ID',
        align: 'start',
        sortable: false,
        value: 'id'
      },
      {
        text: 'GUID',
        align: 'start',
        sortable: false,
        value: 'guid'
      },
      { text: 'Имя', value: 'name', sortable: false },
      { text: 'Фамилия', value: 'surname', sortable: false },
      { text: 'Подразделение', value: 'department', sortable: false },
      { text: 'Дата регистрации', value: 'date', sortable: false },
      { text: '', value: 'actions', sortable: false }
    ],
    rieltors: [],
    editedIndex: -1,
    editedItem: {
      id: null,
      guid: '',
      name: '',
      surname: '',
      department: '',
      date: ''
    },
    defaultItem: {
      id: null,
      guid: '',
      name: '',
      surname: '',
      department: '',
      date: ''
    }
  }),
  computed: {
    formTitle () {
      return this.editedIndex === -1 ? 'New Item' : 'Edit Item'
    }
  },

  watch: {
    dialog (val) {
      val || this.close()
    }
  },

  created () {
    this.initialize()
  },

  methods: {
    initialize () {
      this.rieltors = [
        {
          id: 1,
          guid: 'dsaad',
          name: 'Валера',
          surname: 'Иванов',
          department: 'ЮМР',
          date: '01.01.2000'
        },
        {
          id: 2,
          guid: 'sds',
          name: 'Петя',
          surname: 'Петров',
          department: 'ФМР',
          date: '01.01.2000'
        },
        {
          id: 3,
          guid: 'sdsssa',
          name: 'Игорь',
          surname: 'Сидоров',
          department: 'ЦМР',
          date: '01.01.2000'
        }
      ]
    },

    editItem (item) {
      this.editedIndex = this.rieltors.indexOf(item)
      this.editedItem = Object.assign({}, item)
      this.dialog = true
    },

    deleteItem (item) {
      const index = this.rieltors.indexOf(item)
      confirm('Вы уверены, что хотите удалить?') && this.rieltors.splice(index, 1)
    },

    close () {
      this.dialog = false
      this.$nextTick(() => {
        this.editedItem = Object.assign({}, this.defaultItem)
        this.editedIndex = -1
      })
    },

    save () {
      if (this.editedIndex > -1) {
        Object.assign(this.rieltors[this.editedIndex], this.editedItem)
      } else {
        this.rieltors.push(this.editedItem)
      }
      this.close()
    }
  }
}
</script>

<style scoped>

</style>
