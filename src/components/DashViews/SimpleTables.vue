<template>
  <v-container
    fill-height
    fluid
    grid-list-xl
  >
    <v-layout
      justify-center
      wrap
    >

      <v-flex
        md12
      >

        <material-card
          color="general"
          title="Broadcast Table"
          text=""
        >
          <v-btn
            color="general"
            dark
            class="mb-2" >New Broadcast</v-btn>
          <v-dialog
                  v-model="dialog"
                  max-width="500px">
            <template v-slot:activator="{ on }">
              <v-btn
                      color="general"
                      dark
                      class="mb-2"
                      v-on="on">New Item</v-btn>
            </template>

            <v-card>
              <v-card-text>
                <v-container grid-list-md >
                  <v-layout wrap>
                    <v-flex
                            xs12
                            sm6
                            md4>
                      <v-text-field
                              v-model="editedItem.username"
                              label="Username" />
                    </v-flex>
                    <v-flex
                            xs12
                            sm6
                            md4>
                      <v-text-field
                              v-model="editedItem.password"
                              label="Password" />
                    </v-flex>
                    <v-flex
                            xs12
                            sm6
                            md4>
                      <v-text-field
                              v-model="editedItem.email"
                              label="Email"/>
                    </v-flex>
                    <v-flex
                            xs12
                            sm6
                            md4>
                      <v-checkbox v-model="checkboxAdmin" :label="`IsAdmin`"></v-checkbox>

                    </v-flex>
                    <v-flex
                            xs12
                            sm6
                            md4>
                      <v-checkbox v-model="checkboxActive" :label="`IsActive`"></v-checkbox>
                    </v-flex>
                  </v-layout>
                </v-container>
              </v-card-text>

              <v-card-actions>
                <v-spacer/>
                <v-btn
                        color="blue darken-1"
                        flat
                        @click="close">Cancel</v-btn>
                <v-btn
                        color="blue darken-1"
                        flat
                        @click="save">Save</v-btn>
              </v-card-actions>
            </v-card>
          </v-dialog>
          <v-data-table
            :headers="headers"
            :items="items"
            hide-actions
          >
            <template
              slot="headerCell"
              slot-scope="{ header }"
            >
              <span
                class="subheading font-weight-light text-general text--darken-3"
                v-text="header.text"
              />
            </template>
            <template
              slot="items"
              slot-scope="{ item }"
            >
              <td>{{ item.title }}</td>
              <td>{{ item.body }}</td>
              <td>{{ item.desc }}</td>
              <td>{{ item.id }}</td>
              <!--<td class="text-xs-right">{{ item.salary }}</td>-->
            </template>
          </v-data-table>
        </material-card>
      </v-flex>

      <!--<v-flex-->
        <!--md12-->
      <!--&gt;-->
        <!--<material-card-->
          <!--color="general"-->
          <!--flat-->
          <!--full-width-->
          <!--title="Table on Plain Background"-->
          <!--text="Here is a subtitle for this table"-->
        <!--&gt;-->
          <!--<v-data-table-->
            <!--:headers="headers"-->
            <!--:items="items.slice(0, 7)"-->
            <!--hide-actions-->
          <!--&gt;-->
            <!--<template-->
              <!--slot="headerCell"-->
              <!--slot-scope="{ header }"-->
            <!--&gt;-->
              <!--<span-->
                <!--class="subheading font-weight-light text-general  text&#45;&#45;darken-3"-->
                <!--v-text="header.text"-->
              <!--/>-->
            <!--</template>-->
            <!--<template-->
              <!--slot="items"-->
              <!--slot-scope="{ item }"-->
            <!--&gt;-->
              <!--<td>{{ item.name }}</td>-->
              <!--<td>{{ item.country }}</td>-->
              <!--<td>{{ item.city }}</td>-->
              <!--<td class="text-xs-right">{{ item.salary }}</td>-->
            <!--</template>-->
          <!--</v-data-table>-->
        <!--</material-card>-->
      <!--</v-flex>-->
    </v-layout>
  </v-container>
</template>

<script>
    import {
        mapMutations,
        mapState
    } from 'vuex'
export default {
  data: () => ({
    headers: [
      {
        sortable: false,
        text: 'Title',
        value: 'title'
      },
      {
        sortable: false,
        text: 'Body',
        value: 'body'
      },
      {
        sortable: false,
        text: 'Description',
        value: 'description'
      },
        {
            sortable: false,
            text: 'ID',
            value: 'id'
        }
    ]
  }),
    computed: {
        items () {
//            console.log(this.$store.state.broadcasts);
            return this.$store.getters.getAllBroadcasts;
        }
    },
    mounted () {
        this.$store.dispatch('getBroadcasts')
            .then((response) => console.log('hi'))
            .catch(err => {
                    console.log(err)
                    this.snackbar= true
                }
            )
    }
}
</script>
