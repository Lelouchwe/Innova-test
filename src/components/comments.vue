<template>
  <div class="container">
        <commentsItem 
            v-for="(item, index) in commentsToShow" :key="index"
            :item="comments[index]"
            :toggle="true"
            :childs="childComments"
        />
        <div v-if="commentsToShow < totalComments" class="show-more" @click="addToShow">
            Показать еще
        </div>
  </div>
</template>

<script>
import commentsJson from "@/comments2.json"
export default {
    components: {
        commentsItem: () => import('@/components/commentsItem.vue')
    },
    data() {
        return {
            commentsToShow: 3,
        }
    },
    computed: {
            comments(){
                return commentsJson.filter( item => !item.parentId)
            },
            childComments(){
                return commentsJson.filter( item => item.parentId)
            },
            totalComments(){
                return this.comments.length
            }
    },
    methods: {
            addToShow(){
                this.commentsToShow + 3 <= this.totalComments ? 
                this.commentsToShow += 3 : 
                this.commentsToShow += this.totalComments-this.commentsToShow
            },
            setSpoiler(id){
                console.log(id);
                // let item = this.childComments.find( item => item.id === id)
                console.log(this.childComments);
                // return item.spoiler = !item.spoiler
            }
    }

}
</script>

<style>
h1, p {
    text-align: left;
}
.sub-comments {
    margin: 0 0 0 20px;
}
.show-more {
    margin-top: 20px;
    cursor: pointer;
}
.show-more:hover {
    opacity: .8;
}
</style>