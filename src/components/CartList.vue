<script setup>
import { ref, defineProps, defineEmits } from 'vue';

const props = defineProps(['cartList','total','note']);

const emit = defineEmits(['del-item', 'send-order']);

//購物車備註
const note = ref('');

//送出
const emitSendOrder = () => {
  emit('send-order', note.value);
  //清空備註
  note.value = '';
}

</script>

<template>
  <div class="col-md-8">
    <table class="table">
      <thead>
        <tr>
          <th scope="col" width="50">操作</th>
          <th scope="col">品項</th>
          <th scope="col">描述</th>
          <th scope="col" width="90">數量</th>
          <th scope="col">單價</th>
          <th scope="col">小計</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in props.cartList" :key="item.id">
          <td><button type="button" class="btn btn-sm" @click.prevent="emit('del-item', item.id)">x</button></td>
          <td>{{ item.name }}</td>
          <td><small>{{ item.description }}</small></td>
          <td>
            <select class="form-select" v-model="item.qty">
              <option value="1">1</option>
              <option value="2">2</option>
              <option value="3">3</option>
              <option value="4">4</option>
              <option value="5">5</option>
              <option value="6">6</option>
              <option value="7">7</option>
              <option value="8">8</option>
              <option value="9">9</option>
              <option value="10">10</option>
            </select>
          </td>
          <td>{{ item.price }}</td>
          <td>{{ item.price * item.qty }}</td>
        </tr>
      </tbody>
    </table>
    <div v-if="props.cartList == 0" class="alert alert-primary text-center" role="alert">
      請選擇商品
    </div>
    <div v-else>
      <div class="text-end mb-3">
        <h5>總計: <span>${{ props.total }}</span></h5>
      </div>
      <textarea
        class="form-control mb-3"
        rows="3"
        placeholder="備註"
        v-model="note"
      ></textarea>
      <div class="text-end">
        <button class="btn btn-primary" @click="emitSendOrder">送出</button>
      </div>
    </div>
  </div>
</template>
