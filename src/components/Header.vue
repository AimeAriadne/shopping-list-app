<template>
    <div id="header">
        <h1>{{ header }}</h1>
        <button v-if="editing" @click="$emit('doNotEdit')" class="btn-cancel">Cancel</button>
        <button v-else @click="$emit('doEdit')" class="btn-new">New Items</button>
    </div>
</template>

<script>
export default {
    name: 'Header',
    props: {
        editing: Boolean
    },
    data() {
        return {
            header: 'Shopping List App',
        }
    },
}
</script>

<style scoped>
#header {
  display: flex;
  justify-content: space-evenly;
  align-items: center;
}
</style>