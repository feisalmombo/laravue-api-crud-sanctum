<template>
    <div>
        <h4 class="text-center">Show Book</h4>
        <div class="container">
            <div class="row">
                <div class="col-md-12">
                    <form>
                        <div class="form-group">
                            <label>Name</label>
                            <input type="text" class="form-control" v-model="book.name">
                        </div><br>
                        <div class="form-group">
                            <label>Author</label>
                            <input type="text" class="form-control" v-model="book.author">
                        </div><br>
                    </form>
                </div>
            </div>
        </div>
    </div>
</template>

<script>

export default {
    data() {
        return {
            book: {}
        }
    },
    created() {
        this.$axios.get('/sanctum/csrf-cookie').then(response => {
            this.$axios.get(`/api/books/show/${this.$route.params.id}`)
                .then(response => {
                    // console.log(this.book = response.data)
                    this.book = response.data;
                })
                .catch(function (error) {
                    console.error(error);
                });
        })
    },
    methods: {
    },
    beforeRouteEnter(to, from, next) {
        if (!window.Laravel.isLoggedin) {
            window.location.href = "/";
        }
        next();
    }
}
</script>
