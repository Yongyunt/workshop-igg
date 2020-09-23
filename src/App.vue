<template>
  <v-app>
    <div>
    <Navbar></Navbar>
    </div>
    <v-main>
      <v-layout>
        <v-container>
          <router-view/>
        </v-container>
      </v-layout>
    </v-main>
  </v-app>
</template>

<script>
import Navbar from './components/Navbar';

export default {
  name: 'App',
  components: {
    Navbar,
  },
  data: () => ({}),
  methods: {
    async gotoBuy() {
      await this.$router.push({
        name: "Buy",
      })
    }
  },
}
</script>