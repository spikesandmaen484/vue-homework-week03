<script setup>
import { computed, ref } from 'vue';
import ProductMenu from './components/ProductMenu.vue';
import CartList from './components/CartList.vue';
import OrderList from './components/OrderList.vue';

//飲料主選單項目資料
const data = [
  {
    "id": 1,
    "name": "珍珠奶茶",
    "description": "香濃奶茶搭配QQ珍珠",
    "price": 50
  },
  {
    "id": 2,
    "name": "冬瓜檸檬",
    "description": "清新冬瓜配上新鮮檸檬",
    "price": 45
  },
  {
    "id": 3,
    "name": "翡翠檸檬",
    "description": "綠茶與檸檬的完美結合",
    "price": 55
  },
  {
    "id": 4,
    "name": "四季春茶",
    "description": "香醇四季春茶，回甘無比",
    "price": 45
  },
  {
    "id": 5,
    "name": "阿薩姆奶茶",
    "description": "阿薩姆紅茶搭配香醇鮮奶",
    "price": 50
  },
  {
    "id": 6,
    "name": "檸檬冰茶",
    "description": "檸檬與冰茶的清新組合",
    "price": 45
  },
  {
    "id": 7,
    "name": "芒果綠茶",
    "description": "芒果與綠茶的獨特風味",
    "price": 55
  },
  {
    "id": 8,
    "name": "抹茶拿鐵",
    "description": "抹茶與鮮奶的絕配",
    "price": 60
  }
];

//購物車清單
const cartList = ref([]);

//訂單清單
const orderList = ref([]);

//訂單備註
const orderNote = ref('');


//加入購物車
const addCart = (prod) => {
  const index = cartList.value.findIndex((item) => item.id === prod.id);
  //若購物車無此項才加入
  if (index == -1) {
    cartList.value.push({...prod, qty: 1});
  }
  else {
    alert('此項商品已加入購物車!');
  }
}

//刪除購物車選項
const delItem = (id) => {
  const index = cartList.value.findIndex((item) => item.id === id);
  if (index != -1) {
    cartList.value.splice(index, 1);
  }
}

//送出
const sendOrder = (note) => {
  orderList.value = [...cartList.value];
  orderNote.value = note;

  //清空購物車
  cartList.value = [];
}

//計算總金額-購物車
const total = computed(() => {
  return cartList.value.reduce((sum, item) => sum + item.price * item.qty, 0);
});

//計算總金額-訂單
const orderTotal = computed(() => {
  return orderList.value.reduce((sum, item) => sum + item.price * item.qty, 0);
});
</script>

<template>
  <div id="root">
    <div class="container mt-5">
      <div class="row">
        <div class="col-md-4">
          <div class="list-group">
            <ProductMenu :data="data" @add-cart="addCart" @del-item="delItem" />
          </div>
        </div>
        <CartList :cart-list="cartList" :total="total" :note="note" @del-item="delItem" @send-order="sendOrder" />
      </div>
      <hr />
      <div class="row justify-content-center">
        <OrderList :order-list="orderList" :order-total="orderTotal" :order-note="orderNote" />
      </div>
    </div>
  </div>
</template>
