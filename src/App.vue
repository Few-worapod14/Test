<template>
  <v-app>
    <v-app-bar app lighten>
      <div class="d-flex align-center pl-10 pa-2">
        <h2 class="light-blue--text text--darken-4 text-company">Shiba Book Shop</h2>
      </div>
      <v-spacer></v-spacer>
      <div class="pa-2" v-if="count == '0'">
        <v-icon color="light-blue darken-4">shopping_cart
        </v-icon>
      </div>
      <div class="pa-2" v-else>
        <v-badge color="error" :content="this.count" tile overlap>
          <v-icon color="light-blue darken-4">shopping_cart
          </v-icon>
        </v-badge>
      </div>
      <div class="pa-2 pr-10 cursor" @click="drawer = !drawer">
        <strong class="light-blue--text text--darken-4 text-company">฿ {{total()}}</strong>
      </div>
    </v-app-bar>
    <v-navigation-drawer app v-model="drawer" right width="500px">
      <!-- <template v-slot:prepend> -->
      <v-list-item>
        <v-icon @click="drawer = !drawer" class="hidden-md-and-up">arrow_back</v-icon>
        <h2 class="light-blue--text text--darken-4 pl-3">Cart</h2>

      </v-list-item>
      <!-- </template> -->
      <v-container>

        <!-- <v-simple-table fixed-header height="300px">
          <template v-slot:default>
            <thead>
              <tr>
                <th class="text-center hidden-sm-and-down">

                </th>
                <th class="text-center">
                  Title
                </th>
                <th class="text-center">
                  Price
                </th>
                <th class="text-center">
                  Amount
                </th>
                <th class="text-center">
                  Total
                </th>
                <th class="text-center">

                </th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="item in cards">
                <td class="hidden-sm-and-down">
                  <v-img :src="item.cover" class="img-card "></v-img>
                </td>
                <td class="text-center">{{ item.title }}</td>
                <td class="text-center">{{ item.price }}</td>
                <td class="text-center" width="100%">
                  <v-icon @click="removeqty(item)" class="icon">remove</v-icon>
                  {{ item.qty }}
                  <v-icon @click="addqty(item)" class="icon">add</v-icon>


                </td>
                <td class="text-center">{{ item.total }}</td>
                <td class="text-center">
                  <v-icon @click="remove(item)">delete</v-icon>
                </td>
              </tr>
            </tbody>
          </template>
        </v-simple-table> -->
        <div class="p-2">
          <v-row>
            <v-col xs='4' sm="4" md="4" lg="4">
              <h4 class="text-center">Title</h4>
            </v-col>
            <v-col xs='2' sm="2" md="2" lg="2">
              <h4 class="text-center">Price</h4>
            </v-col>
            <v-col xs='3' sm="3" md="3" lg="3">
              <h4 class="text-center">Amount</h4>
            </v-col>
            <v-col xs='2' sm="2" md="2" lg="2">
              <h4 class="text-center">Total</h4>
            </v-col>
            <v-col xs='1' sm="1" md="1" lg="1">

            </v-col>
          </v-row>
          <v-list v-for="item in cards">
            <v-row>
              <v-col xs='4' sm="4" md="4" lg="4">
                <p>{{ item.title }}</p>
              </v-col>
              <v-col xs='2' sm="2" md="2" lg="2">
                <p class="text-center">{{ item.price }}</p>
              </v-col>
              <v-col xs='3' sm="3" md="3" lg="3">
                <div class="text-center">
                <v-icon @click="removeqty(item)" class="icon">remove</v-icon>
                {{ item.qty }}
                <v-icon @click="addqty(item)" class="icon">add</v-icon> 
              </div>
              </v-col>
           
              <v-col xs='2' sm="2" md="2" lg="2">
                <p class="text-center">{{ item.total }}</p>
              </v-col>
              <v-col xs='1' sm="1" md="1" lg="1">
                <v-icon @click="remove(item)">delete</v-icon>
              </v-col>
            </v-row>
          </v-list>
          <v-row>
            <v-col xs='6' sm="6" md="6" lg="6">
              <h4 class="text-right">Discount :</h4>
            </v-col>
            <v-col xs='6' sm="6" md="6" lg="6">
             <h4>฿ {{total()}}</h4> 
            </v-col >
          </v-row>
        <v-row>
            <v-col xs='6' sm="6" md="6" lg="6">
              <h4 class="text-right">Net :</h4>
            </v-col>
            <v-col xs='6' sm="6" md="6" lg="6">
             <h4>฿ {{total()}}</h4> 
            </v-col>
           
          </v-row>
          
        </div>
      </v-container>
    </v-navigation-drawer>
    <v-main class="background-body">
      <v-container>
        <v-row v-for="item in data">
          <v-col xs='6' sm="6" md="3" lg="3" v-for="items in item">
            <v-hover v-slot="{ hover }" close-delay="">
              <v-card class="mx-auto pa-3" :elevation="hover ? 16 : 2">
                <v-img :src="items.cover" class="img"></v-img>
                <v-card-text>
                  <h4 v-text="items.title"></h4>
                </v-card-text>
                <v-card-text>
                  <h3 v-text="'฿ '+ items.price + '.00'"></h3>
                </v-card-text>

                <v-card-action>

                  <v-btn block color="warning" @click="addCard(items)">
                    <v-icon>shopping_cart</v-icon>add to cart
                  </v-btn>
                </v-card-action>
              </v-card>
            </v-hover>
          </v-col>
        </v-row>
      </v-container>

      <!-- <v-snackbar v-model="snackbar" right color="success" class="snackbar" :timeout="timeout">
        <v-alert type="success" class="alert">
          Add To Card Success
        </v-alert>

      </v-snackbar> -->


    </v-main>
  </v-app>
</template>

<script>
  export default {
    name: 'App',

    components: {

    },

    data: () => ({
      drawer: false,
      data: {},
      cards: [],
      count: 0,
      count1: 0,
      snackbar: false,
      timeout: 2000,

      //
    }),
    mounted() {
      this.getdata()
    },
    methods: {
      getdata() {
        this.axios.get('https://akita-examination.s3-ap-southeast-1.amazonaws.com/shiba-book-shop.json', {
        }).then((response) => {
          if (response.status == 200) {
            this.data = response.data
          }
        })
      },
      addCard: function (item) {
        var id = item.id
        let existID = this.cards.map(i => { return i.id });
        if (existID.includes(item.id)) {
          var found = this.findIndex(item)
          this.cards[found].qty += 1;
          this.cards[found].total = this.cards[found].qty * this.cards[found].price;
          this.snackbar = true
         
        }
        else {
          this.pushData(item)
          this.count +=1
          this.snackbar = true
        }
        // let tmp = this.cards ;
        // let newCard = this.cards.map(el =>{
        //   if(el.id == item.id){
        //     el.qty += 1;
        //     el.total = el.qty * el.price;
        //   }
        //   else{
        //     this.pushData(item) ; 
        //   }
        //   return el ;
        // });
        // this.cards = newCard;
        // if (item.id == '9781408855652') {
        //   this.count += 1;
        //   if (this.count <= 1) {
        //     this.pushData(item)
        //   } else {
        //     var found = this.findIndex(item)
        //     this.cards[found].qty += 1;
        //     this.cards[found].total = this.cards[found].qty * this.cards[found].price;
        //   }
        // } else if (item.id == '9781408855669') {
        //   this.count1 += 1;
        //   if (this.count1 <= 1) {
        //     this.pushData(item)
        //   } else {
        //     var found = this.findIndex(item)
        //     this.cards[found].qty += 1;
        //     this.cards[found].total = this.cards[found].qty * this.cards[found].price;
        //   }
        // }
      },
      pushData(product) {
        this.cards.push({
          id: product.id,
          cover: product.cover,
          title: product.title,
          price: product.price,
          qty: 1,
          total: product.price
        })
      },
      findIndex: function (item) {
        for (var i = 0; i < this.cards.length; i++) {
          if (this.cards[i].id == item.id) {
            return i;
          }
        }
        return -1;
      },
      removeqty: function (items) {
        items.qty -= 1;
        if (items.qty <= 1) {
          items.qty = 1;
        }
        items.total = items.price * items.qty
      },
      addqty: function (items) {
        items.qty += 1;
        items.total = items.price * items.qty
      },
      remove(items) {
        var index = this.cards.indexOf(items);
        this.cards.splice(index, 1)
        this.count = 0
      },
      total: function () {
        var sum = 0;
        this.cards.forEach(function (item) {
          sum = parseInt(parseInt(sum) + parseInt(item.total));
        });
        return sum
      },
      Discount : function () {
        var sum = 0;
        this.cards.forEach(function (item) {
          sum = parseInt(parseInt(sum) + parseInt(item.total));
        });
        return sum
      }


    },
  };
</script>
<style scoped="">
  .background-body {
    background-color: #f8f8f8;
  }
  .cursor {
    cursor : pointer
  }
  .cursor :hover {
    cursor : pointer;
    font-size: 20px;
    color: #D50000 !important;
  }
  .img {
    max-width: 170px;
    width: 100%;
    height: 250px;
    display: block;
    margin: auto;
  }

  .img-card {
    max-width: 30px;
    width: 100%;
    height: 60px;
    display: block;
    margin: auto;
  }

  .snack {
    margin-right: 0px !important;
    padding: 0px !important;

  }
  .alert {
    margin-bottom: 0px !important;
    padding: 0px !important;
  }

  @media (max-width: 600px) {
    p {
      font-size: 10px !important;
    }

    .icon {
      font-size: 12px !important;
    }
    .text-company {
      font-size: 15px;
    }
    h4 {
      font-size: 14px;
    }
  }
</style>