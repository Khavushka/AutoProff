<template>
    <div class="user">
        <div>
            <div> <strong>Afdeling: </strong>{{ user.company }} </div>
            <div> <strong>Navn: </strong>{{ user.name }} </div>
            <div> <strong>Title: </strong>{{ user.title }} </div>
            <div> <strong>Telefonnr.: </strong> {{ user.phone }}</div>
        </div>
        <div class="user__btns">
            <my-button @click="$emit('remove', user)">slet</my-button>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        user: {
            type: Object,
            required: true,
        }
    }
}
</script>

<style scoped>
    .user {
        padding: 15px;
        border: 2px solid grey;
        margin-top: 15px;
        display: flex;
        align-items: center;
        justify-content: space-between;
    }
</style>