<template>
    <div class="container">
        <div class="comment-item">
            <h1>{{item.name}}</h1>
            <p>{{item.content}}</p>
        </div>
        <div class="child-comment" v-if="item.child">
            <commentsItem 
                v-for="(sub, index) in item.child" :key="index" 
                class="sub-comments"
                :item="sub"
            />
        </div>
    </div>
</template>

<script>
export default {
    name: 'commentsItem',
    props: ['item'],
    data() {
        return {
        }
    },
    methods: {

    }

}
</script>

<style>
.sub-comments {
  margin: 0 20px;
}
.show-more {
  cursor: pointer;
}
.show-more:hover {
  opacity: .8;
}
.comment-item {
    padding: 10px;
    transition: .3s;
    border-radius: 10px;
}
.comment-item:hover {
    background: #8080800c;
}
.child-comment {
    border-left: 1px solid #80808063;
}
</style>