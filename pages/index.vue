<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <v-card>
        <v-card-title class="headline">
          Welcome NuxtJS & Firebase
        </v-card-title>
        <v-card-text>
          <ul>
            <li v-for="user in users" :key="user.id">
              {{ user.id }} - {{ user.name }}
            </li>
          </ul>
        </v-card-text>
        <v-card-actions>
          <v-spacer />
          <v-btn
            color="primary"
            @click="load()"
          >
            Load
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  data () {
    return {
      users: []
    }
  },
  methods: {
    load () {
      this.users = []

      const result = this.$fire.firestore.collection('users').get()

      result.then((snapshot) => {
        snapshot.docs.forEach((element) => {
          this.users.push({
            ...{ id: element.id },
            ...element.data()
          })
        })
      })
    }
  }
}
</script>
