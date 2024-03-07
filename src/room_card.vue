<template>
    <div>
        <img :src="room.image" class="room-image" />
        <!--<h4 @click="room_info_window.is_open = true; room_info_window.room = room"> {{ room.title }} </h4>-->
        <p> {{ distinguish_with_commas(room.price) }} 원 </p>
    </div>
</template>

<script>
export default {
    name: 'RoomCard',
    props: {
        room: Object,
        room_info_window: Object,
        distinguish_with_commas: Function,
    }
}
</script>

<style>
.room-image {
    width: 50%;
    margin-top: 40px;
}
</style>