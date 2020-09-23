<template>
  <div >
    <!-- button -->
    <div class="d-flex justify-end ">
      <div>
        <v-select
            v-model = 'datacoin'
            :items="items"
            label="coin"
        ></v-select>
      </div>
      <v-btn @click="getdatacoin"
          large
          color="white"
      >
        Select
      </v-btn>
    </div>
    <div class="d-flex justify-end ">
      <h1 v-if="!dialog">{{result}} บาท</h1>
    </div>
    <!-- show -->
    <div class="d-flex flex-wrap ">
      <div v-for="d in drink" :key="d.id">
        <v-card
            class=" ma-5"
            max-width="300px"
            max-height="300px"
        >
          <v-img
              class="white--text align-end"
              height="200px"
              :src="d.image"
          >
          </v-img>
          <v-card-text>
            {{d.name}}
            {{d.price}}
          </v-card-text>
          <div class="d-flex justify-end " >
            <v-btn @click="Changecoin(d.price)"
                   :disabled="d.price > result"
                large
                color="#3F51B5"
            >
              Buy
            </v-btn>
          </div>

        </v-card>
      </div>




    </div>
    <template>
      <div class="text-center">
        <v-dialog
            v-model="dialog"
            width="500"
        >


          <v-card>
            <v-card-title class="headline grey lighten-2">
             ชำระเสร็จสิ้น
            </v-card-title>

            <v-card-text>
              ยอดคงเหลือ {{result}}
            </v-card-text>

            <v-divider></v-divider>

            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn
                  color="primary"
                  text
                  @click="dialog = false"
              >
                I accept
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </div>
    </template>
  </div>
</template>

<script>
import axios from 'axios'


export default {
  name: 'Home',
  components: {},
  data: () => ({
    drink: null,
    coin: null,
    items: [1, 2, 5, 10],
    result:0,
    datacoin: null,
    Change:null,
    dialog: false
  }),
  async created() {
    await this.getdata()
  },
  methods: {
    getdatacoin () {
      this.result += this.datacoin
    },
    Changecoin (price) {
      this.result -= price


      
      this.dialog = true
    },
    async gotoBuy() {
      await this.$router.push({
        name: "Buy",
      })
    },
    async getdata () {
      this.drink = await axios.get(`https://www.mocky.io/v2/5c77c5b330000051009d64c9`)
          .then((res) => {
            console.log(res.data)
            return res.data.data
          })
    }

  },
}
</script>