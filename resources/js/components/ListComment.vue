<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-12">
                <div class="card">
                    <div class="card-header">Deixe um comentário!</div>
                    <div class="card-body">
                        <form-comment v-on:add-comment="addComment"></form-comment>
                        <view-comment v-on:remove-comment="removeComment" v-model="allComments" :allComments="allComments"></view-comment>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import FormComment from "./FormComment";
    import ViewComment from "./ViewComment";

    export default {
        components: {
            FormComment,
            ViewComment
        },
        data() {
            return {
                comments: []
            }
        },
        methods: {
            async addComment(comment) {
                const { data } = await window.axios.post('/api/comment', comment);
                this.comments.push(data);
            },
            async removeComment(comment) {
                if (confirm("Você deseja excluir o registro?")) {
                    await window.axios.delete('/api/comment/' + comment.id);
                    let index = this.comments.findIndex(crud => crud.id === comment.id);
                    this.comments.splice(index, 1);
                }
            },
            async read() {
                const { data } = await window.axios.get('/api/comment');
                data.forEach(comment => this.comments.push(comment));
            }
        },
        created() {
            this.read();
        },
        computed: {
            allComments() {
                return this.comments.map(comment => ({
                    ...comment,
                    name: comment.name.trim() === '' ? 'Anônimo' : comment.name
                }));
            }
        }
    }
</script>
