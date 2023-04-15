<template>
    <footer>
        <a href="/">Codeforces</a> &copy; 2021 by Mike Mirzayanov
        users {{ usersCount }}
        posts {{ postsCount }}
    </footer>
</template>

<script>
export default {
    name: "Footer",
    props: ["usersCount", "postsCount"]
}
</script>

<style scoped>

</style>