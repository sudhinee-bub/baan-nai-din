<template>
  <div>
    <v-row dense class="d-flex flex-wrap">
      <v-col v-for="item in items" :key="item.title" cols="12" lg="4" sm="6">
        <v-card
          class="mx-auto"
          max-width="355"
          min-height="197"
          outlined
          :color="item.quantity > 0 ? 'info':''"
        >
          <v-list-item three-line class="store">
            <v-list-item-content>
              <v-list-item-title class="text-h5 mb-1">
                {{item.bookname}}
              </v-list-item-title>
              <v-list-item-subtitle>{{item.bookname}}</v-list-item-subtitle>
              <div class="text-overline mb-4">
                ฿ {{item.price}}
              </div>
            </v-list-item-content>
      
            <v-list-item-avatar
              tile
              size="120"
              color="grey"
            >
              <v-img contain :src="item.image"></v-img>
            </v-list-item-avatar>
          </v-list-item>
      
          <v-card-actions>
            <v-btn color="primary"
              fab
              x-small
              @click="item.quantity--">
              <v-icon small>mdi-minus</v-icon>
            </v-btn>
              <v-text-field
                v-model="item.quantity"
                outlined
                dense
                rounded
                class="mx-1 my-0 py-0"
                hide-details="auto"
              ></v-text-field>
            <v-btn color="primary" 
              fab
              x-small
              @click="item.quantity++">
              <v-icon small>mdi-plus</v-icon>
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
    <v-dialog
      v-model="dialog"
      persistent
      scrollable
      transition="dialog-bottom-transition"
      width="600"
    >
      <template #activator="{ on, attrs }">
        <v-btn
          v-show="checkSumQty"
          v-bind="attrs"
          color="secondary"
          elevation="4"
          class="my-4 mx-4"
          fixed
          fab
          large
          bottom
          right
          v-on="on"
          @click="openCart"
        >
          <v-icon color="black"> mdi-cart </v-icon>
        </v-btn>
      </template>
      <v-card>
        <v-toolbar dark color="primary">
          <v-btn icon dark @click="closeCart">
            <v-icon>mdi-close</v-icon>
          </v-btn>
          <v-toolbar-title>ตะกร้าสินค้า</v-toolbar-title>
          <v-spacer></v-spacer>
        </v-toolbar>
        <v-card-text style="height: 400px">
          <v-list v-for="(book, index) in carts" :key="index"> 
            <v-list-item three-line>
              <v-list-item-content>
                <v-list-item-title>{{ book.bookname }}</v-list-item-title>
                <v-list-item-subtitle>จำนวน {{ book.quantity }} เล่ม</v-list-item-subtitle>
              </v-list-item-content>
              <v-list-item-avatar
                tile
                size="60"
                color="grey"
              >
                <v-img contain :src="book.image"></v-img>
              </v-list-item-avatar>
            </v-list-item>
            <v-divider></v-divider>
          </v-list>
            <v-list-item three-line fixed>
              <v-list-item-content class="text-right">
                <v-list-item-title>รวมเงินทั้งสิ้น {{ sumPrice }} บาท</v-list-item-title>
                <v-list-item-subtitle>จำนวน {{ sumQty }} เล่ม</v-list-item-subtitle>
                <v-list-item-subtitle>ส่วนลด {{ discount }} บาท</v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>
        </v-card-text>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
// import ShoppingCart from './shoppingcart.vue'
export default {
  name: 'IndexPage',
  data: () => ({
    dialog: false,
    items: [
      {
        bookname: 'แฮร์รี่ พอตเตอร์กับศิลาอาถรรพ์',
        quantity: 0,
        price: 100,
        image:
          'https://www.b2s.co.th/media/catalog/product/cache/31c1e2dc995f93131e503292bcd47775/5/2/5293576_e1.jpg',
        selected: false,
      },
      {
        bookname: 'แฮร์รี่ พอตเตอร์กับห้องแห่งความลับ',
        quantity: 0,
        price: 100,
        image:
          'https://www.b2s.co.th/media/catalog/product/cache/31c1e2dc995f93131e503292bcd47775/5/2/5293577_1.jpg',
        selected: false,
      },
      {
        bookname: 'แฮร์รี่ พอตเตอร์กับนักโทษแห่งอัซคาบัน',
        quantity: 0,
        price: 100,
        image:
          'https://www.b2s.co.th/media/catalog/product/cache/8b3650f0791ec890e72171a526565ea7/5/2/5293578-e1.jpg',
        selected: false,
      },
      {
        bookname: 'แฮร์รี่ พอตเตอร์กับถ้วยอัคนี',
        quantity: 0,
        price: 100,
        image:
          'https://www.b2s.co.th/media/catalog/product/cache/8b3650f0791ec890e72171a526565ea7/5/2/5293579-e1.jpg',
        selected: false,
      },
      {
        bookname: 'แฮร์รี่ พอตเตอร์กับภาคีนกฟีนิกซ์',
        quantity: 0,
        price: 100,
        image:
          'https://www.b2s.co.th/media/catalog/product/cache/8b3650f0791ec890e72171a526565ea7/5/2/5293580-e1.jpg',
        selected: false,
      },
      {
        bookname: 'แฮร์รี่ พอตเตอร์กับเจ้าชายเลือดผสม',
        quantity: 0,
        price: 100,
        image:
          'https://www.b2s.co.th/media/catalog/product/cache/8b3650f0791ec890e72171a526565ea7/5/2/5293581_1.jpg',
        selected: false,
      },
      {
        bookname: 'แฮร์รี่ พอตเตอร์กับเครื่องรางยมทูต',
        quantity: 0,
        price: 100,
        image:
          'https://www.b2s.co.th/media/catalog/product/cache/8b3650f0791ec890e72171a526565ea7/5/2/5293582_1.jpg',
        selected: false,
      },
    ],
    carts: [],
    sumQty: 0,
    sumPrice: 0,
    discount: 0
  }),
  computed: {
    checkSumQty() {
      const sumqty = this.items.reduce((total,item) => { return total + item.quantity},0);
      return sumqty > 0;
    }
  },
  methods: {
    closeCart() {
      this.dialog = false
      this.carts = []
      this.sumQty = 0
      this.sumPrice = 0
    },
    openCart() {
      this.items.forEach((element) => {
        if (element.quantity > 0) {
          this.carts.push(element)
        }
      })

      this.summaryPrice(this.carts)
    },
    summaryPrice(carts) {
      let discount = 0
      switch (carts.length) {
        case 2:
          discount = 10
          break
        case 3:
          discount = 20
          break
        case 4:
          discount = 30
          break
        case 5:
          discount = 40
          break
        case 6:
          discount = 50
          break
        case 7:
          discount = 60
          break
        default:
          discount = 0
      }

      let notsamebookprice = 0
      let samebookprice = 0
      let pricebeforediscount = 0
      carts.forEach((element) => {
        this.sumQty = this.sumQty + element.quantity
        pricebeforediscount = pricebeforediscount + (element.price * element.quantity)
        notsamebookprice = notsamebookprice + element.price
        samebookprice = samebookprice + element.price * (element.quantity - 1)
      })

      notsamebookprice = notsamebookprice - notsamebookprice * (discount / 100)
      this.sumPrice = notsamebookprice + samebookprice
      this.discount = pricebeforediscount - this.sumPrice;
    },
  },
}
</script>
