<template>
    <div class="form-group">
        <p>
            <label>Nome</label>
            <input type="text" name="name" id="name" v-model="name" class="form-control" placeholder="Nome" />
        </p>
        <p>
            <label>Comentário</label>
            <textarea name="message" id="message" v-model="message" class="form-control" placeholder="Comentário"></textarea>
        </p>
        <p>
            <input v-on:click="addComment" type="button" class="btn btn-primary" value="Comentar">
        </p>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                id: '',
                name: '',
                message: ''
            }
        },
        methods: {
            addComment() {
                if (this.name.trim() === '' || this.message.trim() === '') {
                    return;
                }

                this.$emit('add-comment', {
                    name: this.name,
                    message: this.message
                });

                this.name = '';
                this.message = '';
            },
        }
    }
</script>
