<template>
  <div class="container">
        <h1>hello</h1>
        <comments/>
  </div>
</template>

<script>
export default {
    components: {
        comments: () => import('@/components/comments.vue')
    }
}
</script>

<style>

</style>