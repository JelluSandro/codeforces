<template>
    <div class="middle">
        <Sidebar :posts="viewPosts"/>
        <main>
            <Index v-if="page === 'Index'" :posts="reversePosts" :findComments="findComments" :getNick="getNick"/>
            <Enter v-if="page === 'Enter'"/>
            <WritePost v-if="page === 'WritePost'"/>
            <EditPost v-if="page === 'EditPost'"/>
            <Register v-if="page === 'Register'"/>
            <Users v-if="page === 'Users'" :users="users"/>
        </main>
    </div>
</template>

<script>
import Sidebar from "./sidebar/Sidebar";
import Index from "./page/Index";
import Enter from "./page/Enter";
import WritePost from "./page/WritePost";
import EditPost from "./page/EditPost";
import Register from "./page/Register";
import Users from "./page/Users";

export default {
    name: "Middle",
    data: function () {
        return {
            page: "Index"
        }
    },
    components: {
        WritePost,
        Enter,
        Index,
        Sidebar,
        EditPost,
        Register,
        Users
    },
    props: ["posts", "users", "comments"],
    computed: {
        viewPosts: function () {
            return Object.values(this.posts).sort((a, b) => b.id - a.id).slice(0, 2);
        },
        reversePosts: function () {
            return Object.values(this.posts).sort((a, b) => b.id - a.id).slice();
        }
    }, beforeCreate() {
        this.$root.$on("onChangePage", (page) => this.page = page)
    }, methods: {
        findComments: function (id) {
            return Object.values(this.comments).filter(p => p.postId === parseInt(id)).length;
        },
        getNick: function (id) {
            return Object.values(this.users).filter(p => p.id === parseInt(id))[0].login;
        }
    }
}
</script>

<style scoped>

</style>
