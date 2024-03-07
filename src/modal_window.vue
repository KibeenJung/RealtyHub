<template>
    <div v-if="room_info_window.is_open == true" class="black-background">
        <div class="white-background">
            <img :src="room_info_window.room.image" class="room-image" />
            <h4> {{ room_info_window.room.title }} </h4>
            <p> {{ distinguish_with_commas(room_info_window.room.price) }} 원 </p>
            <p> {{ room_info_window.room.content }} </p>
            <!-- <button @click="room_info_window.is_open = false"> 나가기 </button>-->
        </div>
    </div>
</template>

<script>
export default {
    name: 'ModalWindow',
    props: {
        room_info_window: Object,
        distinguish_with_commas: Function,
    },
}
</script>

<style>
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
</style>