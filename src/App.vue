<template>
  <ModalWindow :room_info_window="room_info_window" :distinguish_with_commas="distinguish_with_commas" />
  <Logo />
  <Menu />
  <Discount />
  <RoomCard :room="room" :room_info_window="room_info_window" :distinguish_with_commas="distinguish_with_commas"
    v-for="room in rooms" :key="room" />
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
