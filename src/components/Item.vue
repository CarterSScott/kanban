<template>
    <v-card :color="item.color">
        <v-card-title class="justify-center">
            <span class="h4">{{item.title}}</span>
        </v-card-title>
        <v-card-text>
            <span>{{item.note}}</span>
        </v-card-text>
    </v-card>
</template>

<script>
    export default {
        name: "ItemComponent",
        props: {
            initialTitle: {
                type: String,
                required: true,
            },
            initialNote: {
                type: String,
                required: true,
            },
            initialColor: {
                type: String,
                required: true,
            },
        },
        data() {
            return {
                item: {
                    title: this.initialTitle,
                    note: this.initialNote,
                    color: this.initialColor,
                },
            }
        },
    }
</script>

<style lang="scss" scoped>

</style>