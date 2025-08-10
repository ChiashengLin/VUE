<template>
  <div class="container mt-5">
    <table>
      <thead>
        <tr>
          <th scope="col">品項</th>
          <th scope="col">描述</th>
          <th scope="col">價格</th>
          <th scope="col">庫存</th>
        </tr>
      </thead>
      <tbody>
        <!-- :key 前面的冒號代表是綁定一個變數，不是字串 -->
        <tr v-for="item in beverage" :key="item.id">
          <td>{{ item.name }}</td>
          <td>
            <small>{{ item.description }}</small>
          </td>
          <td>{{ item.price }}</td>
          <td>
            <button @click="handleDrinkStock(item.id, item.stock - 1)" :disabled="item.stock < 1">
              -
            </button>
            {{ item.stock }}
            <button @click="handleDrinkStock(item.id, item.stock + 1)">+</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const data = [
  {
    id: 1,
    name: '珍珠奶茶',
    description: '香濃奶茶搭配QQ珍珠',
    price: 50,
    stock: 20,
  },
  {
    id: 2,
    name: '冬瓜檸檬',
    description: '清新冬瓜配上新鮮檸檬',
    price: 45,
    stock: 15,
  },
  {
    id: 3,
    name: '翡翠檸檬',
    description: '綠茶與檸檬的完美結合',
    price: 55,
    stock: 30,
  },
  {
    id: 4,
    name: '四季春茶',
    description: '香醇四季春茶，回甘無比',
    price: 45,
    stock: 10,
  },
  {
    id: 5,
    name: '阿薩姆奶茶',
    description: '阿薩姆紅茶搭配香醇鮮奶',
    price: 50,
    stock: 25,
  },
  {
    id: 6,
    name: '檸檬冰茶',
    description: '檸檬與冰茶的清新組合',
    price: 45,
    stock: 20,
  },
  {
    id: 7,
    name: '芒果綠茶',
    description: '芒果與綠茶的獨特風味',
    price: 55,
    stock: 18,
  },
  {
    id: 8,
    name: '抹茶拿鐵',
    description: '抹茶與鮮奶的絕配',
    price: 60,
    stock: 20,
  },
]

// 建立了一個可以即時追蹤變化的變數 drinks，它的初始值是 data。
// ref() 是幫變數加上即時監控功能的響應式資料的函式。
// drinks是「包裝起來的變數」，你可以用 drinks.value 去存取或修改裡面的資料。
const beverage = ref(data)

// 這個 handleDrinkStock 函式會根據給定的飲料 id，去更新該飲料的庫存數量（stock）。
function handleDrinkStock(id, stock) {
  beverage.value = beverage.value.map((item) => {
    if (item.id === id) {
      item.stock = stock
      // 把這個飲料的庫存改成新的數字
    }
    return item
  })
}
</script>

<style scoped>
button {
  border-radius: 8px;
  border: 1px solid transparent;
  padding: 0.5em 1em;
  font-size: 1em;
  font-weight: 500;
  font-family: inherit;
  cursor: pointer;
  transition: border-color 0.25s;
}
button:hover {
  border-color: #000000;
}
</style>
