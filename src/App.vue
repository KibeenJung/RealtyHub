<template>
  <transition name="fade">
    <ModalWindow @closeModal="room_info_window.is_open = false" :room_info_window="room_info_window"
      :distinguish_with_commas="distinguish_with_commas" />
  </transition>
  <Logo />
  <Menu />
  <Discount :discount_window="this.discount_window" v-if="discount_window.is_open == true"></Discount>
  <select v-model="sort_option" style="float:left; margin-left: 50px">
    <option value="id"> 번호순</option>
    <option value="price"> 가격낮은순 </option>
    <option value="price_reverse"> 가격높은순 </option>
    <option value="view_count"> 조회순 </option>
  </select>
  <RoomCard @click="room_info_window.is_open = true; room.view_count += 1; room_info_window.room = room" :room="room"
    :room_info_window="room_info_window" :distinguish_with_commas="distinguish_with_commas" v-for="room in rooms"
    :key="room" />
</template>

<script>
import rooms from "./assets/rooms.js";
import Discount from './discount.vue'
import Logo from './logo.vue'
import Menu from './menu.vue'
import ModalWindow from './modal_window.vue'
import RoomCard from './room_card.vue'

export default {
  name: 'App',
  data() {
    return {
      rooms: rooms,
      room_info_window: { is_open: false, room: null },
      discount_window: { is_open: true, discount_percentage: 30 },
      sort_option: 'id'
    }
  },
  mounted() {
    setInterval(() => {
      if (this.discount_window.discount_percentage > 1) {
        this.discount_window.discount_percentage -= 1;
      }
      else {
        this.discount_window.is_open = false;
      }

    }, 1000);
  },
  watch: {
    sort_option(selected_option) {
      if (selected_option === 'id') {
        console.log('id sort')
        this.rooms.sort(function (a, b) { return a.id - b.id })
      }
      else if (selected_option === 'price') {
        console.log('price sort')
        this.rooms.sort(function (a, b) { return a.price - b.price })
      }
      else if (selected_option === 'price_reverse') {
        console.log('price_reverse sort')
        this.rooms.sort(function (a, b) { return b.price - a.price })
      }
      else if (selected_option === 'view_count') {
        console.log('view count')
        this.rooms.sort(function (a, b) { return b.view_count - a.view_count })
      }
    }
  },
  components: {
    Discount: Discount,
    Logo: Logo,
    Menu: Menu,
    ModalWindow: ModalWindow,
    RoomCard: RoomCard,
  },
  methods: {
    distinguish_with_commas: function (number) {
      return number.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ',');
    }
  },
}
</script>

<style>
.fade-enter-from {
  transform: translateY(-1000px)
}

.fade-enter-active {
  transition: all 1s;
}

.fade-enter-to {
  transform: translateY(0px)
}

.fade-leave-from {
  transform: translateY(0px)
}

.fade-leave-active {
  transition: all 1s;
}

.fade-leave-to {
  transform: translateY(-1000px)
}

.select-container {
  display: flex;
  /* Flexbox 사용 */
  align-items: center;
  /* 수직 가운데 정렬 */
}

.select-box {
  margin-right: 10px;
  /* 선택 상자와의 간격 조정 */
}

body {
  margin: 0
}

div {
  box-sizing: border-box;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
