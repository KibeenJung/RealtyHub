<template>
  <div v-if="room_info_window.is_open == true" class="black-background">
    <div class="white-background">
      <img :src="room_info_window.room.image" class="room-image" />
      <h4> {{ room_info_window.room.title }} </h4>
      <p> {{ distinguish_with_commas(room_info_window.room.price) }} 원 </p>
      <p> {{ room_info_window.room.content }} </p>
      <button @click="room_info_window.is_open = false"> 나가기 </button>
    </div>
  </div>

  <Logo></Logo>
  <Menu></Menu>

  <Discount></Discount>

  <div v-for="room in rooms" :key="room">
    <img :src="room.image" class="room-image" />
    <h4 @click="room_info_window.is_open = true; room_info_window.room = room"> {{ room.title }} </h4>
    <p> {{ distinguish_with_commas(room.price) }} 원 </p>
  </div>
</template>

<script>
import rooms from "./assets/rooms.js";
import Discount from './discount.vue'
import Logo from './logo.vue'
import Menu from './menu.vue'

export default {
  name: 'App',
  data() {
    return {
      rooms: rooms,
      room_info_window: { is_open: false, room: null },

    }
  },
  methods: {
    distinguish_with_commas: function (number) {
      return number.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ',');
    }
  },
  created() {
  },
  components: {
    Discount: Discount,
    Logo: Logo,
    Menu: Menu,
  }
}
</script>

<style>
body {
  margin: 0
}

div {
  box-sizing: border-box;
}

.black-background {
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  position: fixed;
  padding: 20px;
}

.white-background {
  width: 100%;
  background: white;
  border-radius: 8px;
  padding: 20px;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.room-image {
  width: 50%;
  margin-top: 40px;
}
</style>
