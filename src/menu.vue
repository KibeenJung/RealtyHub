<template>
    <div class="menu">
        <menu_comp v-for="menu_name in menus" :key="menu_name"> {{ menu_name }}</menu_comp>
    </div>
</template>

<script>
export default {
    name: "Menu",
    data() {
        return {
            menus: ['Home', 'Shop', 'About'],
        }
    }
}
</script>

<style>
.menu {
    background: darkslateblue;
    padding: 15px;
    border-radius: 5px;
}

.menu menu_comp {
    color: white;
    padding: 10px;
}
</style>