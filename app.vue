<template>
  <div>
    <h3>Hello World!</h3>
    <button @click="test()">test</button>
    <br />
    {{ resp }}
  </div>
</template>

<script>
// import jsPDF from "jspdf";
import alasql from 'alasql';

export default {
  data() {
    return {
      resp: 'resp',
    };
  },
  methods: {
    async test() {
      var received = [
        { id: 1, barcode: 'n77', amount: 77 },
        { id: 2, barcode: 'n44', amount: 44 },
        { id: 1, barcode: 'n77', amount: 779 },
        { id: 2, barcode: 'n44', amount: 449 },
        { id: 3, barcode: 'CP07', amount: 9907 },
      ];

      var stock = [
        { id: 1, name: 'Tom', barcode: 'n77', stock: 1, type: 'เสื้อ' },
        { id: 2, name: 'Bob', barcode: 'n44', stock: 2, type: 'กระโปรง' },
        {
          id: 3,
          name: 'Sir Benjamin',
          barcode: 'CP07',
          stock: 3,
          type: 'กางเกง',
        },
      ];

      var res = await alasql(
        'SELECT stock.name AS product_name, received.barcode, received.amount, stock.type FROM ? received LEFT JOIN ? stock ON received.barcode = stock.barcode',
        [received, stock]
      );

      this.resp = JSON.stringify(res);
      // console.log("test")​
    },
  },
};
</script>
