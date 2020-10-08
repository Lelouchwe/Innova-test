<template>
  <div class="container">
        <commentsItem 
            v-for="(item, index) in commentsToShow" :key="index"
            :item="comments[index]"
            :toggle="true"
        />
        <div v-if="commentsToShow < totalComments" class="show-more" @click="addToShow">
            Показать еще
        </div>
  </div>
</template>

<script>
import commentsJson from "@/comments.json"
export default {
  components: {
      commentsItem: () => import('@/components/commentsItem.vue')
  },
  data() {
    return {
        commentsToShow: 3,
        totalComments: 0,
        // deepCounter: 0,
        comments: [],
    }
  },
  computed: {
  },
  methods: {
      addToShow(){
          this.commentsToShow += 3
      },
  },
  mounted() {
      this.totalComments = commentsJson.length
      this.comments = commentsJson
  }

}
</script>

<style>
.sub-comments {
    margin: 0 20px;
}
.show-more {
    margin-top: 20px;
    cursor: pointer;
}
.show-more:hover {
    opacity: .8;
}
</style>