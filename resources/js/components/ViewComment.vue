<template>
    <div class="list-group">
        <p v-if="allComments.length <= 0">Sem comentários...</p>
        <div v-else class="list-group-item" v-for="(comment, index) in allComments" v-bind:key="index">
            <span>Autor: <strong>{{ comment.name }}</strong></span>
            <p>{{ comment.message }}</p>
            <div>
                <a href="#" title="Excluir" v-on:click.prevent="removeComment(comment.id)">Excluir</a>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            allComments: Array
        },
        methods: {
            removeComment(id) {
                this.$emit('remove-comment', {
                    id: id
                });
            }
        }
    }
</script>
