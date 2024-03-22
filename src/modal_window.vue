<template>
    <div v-if="room_info_window.is_open == true" class="black-background">
        <div class="white-background">
            <img :src="room_info_window.room.image" class="room-image" />
            <h4> {{ room_info_window.room.title }} </h4>
            <p> {{ room_info_window.room.content }} </p>
            <span> 계약 기간 (月): </span>
            <!-- <input v-model="month"> -->
            <input v-model="month" type="range" min="1" max="24">
            <p> {{ month }} 개월 사용료: {{ distinguish_with_commas(room_info_window.room.price * month) }} 원 </p>
            <button @click="$emit('closeModal'); month = 1"> 나가기 </button>
        </div>
    </div>
</template>

<script>
export default {
    name: 'ModalWindow',
    data() {
        return {
            month: 1,
        }
    },
    watch: {
        month(value) {
            if (isNaN(value)) {
                alert('문자열을 입력하였습니다.')
                this.month = 1
            }
        }
    },
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