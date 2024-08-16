<script setup>
import { defineProps } from 'vue';

const props = defineProps(['orderList','orderTotal','orderNote']);

</script>
<template>
  <div class="col-8">
    <div v-if="props.orderList.length == 0" class="alert alert-secondary text-center" role="alert">
      尚未建立訂單
    </div>
    <div v-else class="card">
      <div class="card-body">
        <div class="card-title">
          <h5>訂單</h5>
          <table class="table">
            <thead>
              <tr>
                <th scope="col">品項</th>
                <th scope="col">數量</th>
                <th scope="col">小計</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="item in props.orderList" :key="item.id">
                <td>{{ item.name }}</td>
                <td>{{ item.qty }}</td>
                <td>{{ item.price * item.qty }}</td>
              </tr>
            </tbody>
          </table>
          <div class="text-end">備註: <span>{{ props.orderNote }}</span></div>
          <div class="text-end">
            <h5>總計: <span>${{ props.orderTotal }}</span></h5>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
