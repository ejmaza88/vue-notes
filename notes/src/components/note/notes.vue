<template>
    <div>
        <div v-for="(note, index) in notes">
            <div v-bind:key="index">{{note}}</div>
        </div>
    </div>
</template>


<script>
export default {
    name: 'NoteComponent',
    props: ['notes']
}
</script>


<style>

</style>