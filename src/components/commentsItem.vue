<template>
    <div class="container">
        <div class="comment-item">
            <h1>{{item.name}}</h1>
            <p>{{item.content}}</p>
            <div class="comment-nav">
                <div class="comment-nav__answere" @click="answerToggle = !answerToggle">Ответить</div>
            </div>
            <div v-if="answerToggle" class="wrap-answere">
                <textarea 
                    v-model="answerText" 
                    type="text-area" 
                    class="wrap-answere__text" 
                />
                <div class="wrap-answere__nav">
                    <div class="sent btn" @click="sentMessage(item.name)">Отправить</div>
                    <div class="close btn" @click="cancelMessage">Отменить</div>
                </div>
            </div>
        </div>
        <div class="child-comment" v-if="item.child">
            <commentsItem 
                v-for="(sub, index) in item.child" :key="index" 
                class="sub-comments"
                :item="sub"
                :deepCounter="deepCounter"
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
            deepCounter: 0,
            answerToggle: false,
            answerText: '',
        }
    },
    computed: {
        increaseCounter(){
            this.deepCounter++
        }
    },
    methods: {
        sentMessage(parentName) {
            let id = Math.floor(Math.random()*10000)
            let payload = {
                id: id,
                name: `anon#${id}`,
                content: `${parentName}, ${this.answerText}`,
                child: []
            }
            this.item.child.push(payload)
            this.answerText = ''
            this.answerToggle = false
        },
        cancelMessage() {
            this.answerText = ''
            this.answerToggle = false
        }
    },
    mounted(){
        this.deepCounter++
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
.comment-item p {
    font-size: 16px;
}
.comment-item:hover {
    /* background: #8080800c; */
}
.child-comment {
    border-left: 1px solid #80808063;
}
.comment-nav {
    display: flex;
    font-size: 14px;
}
.comment-nav__answere {
    cursor: pointer;
    
}
.comment-nav__answere:hover {
    opacity: .8;
}
.wrap-answere {
    display: flex;
    flex-direction: column;
    border: 1px solid;
    border-radius: 10px;
    padding: 5px;
}
.wrap-answere__text {
    height: 100px;
    margin: 0px;
    border: none;
}
.wrap-answere__nav {
    display: flex;
}
.wrap-answere__nav div {
    margin: 10px;
}
.btn {
  cursor: pointer;
}
.btn:hover {
  opacity: .8;
}
</style>