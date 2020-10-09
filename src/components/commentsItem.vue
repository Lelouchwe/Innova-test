<template>
    <div class="container">
        <div class="comment-item">
            <div class="comment-item__wrap">
                <h1>{{item.name}}</h1>
                <div class="comment-item__likes">
                    <div class="like" @click="setLike">↑</div>
                    <div :style='{color: activeColor}'>{{item.likeCounter}}</div>
                    <div class="dislike" @click="setDislike">↓</div>
                </div>
            </div>
            <p :class="[item.spoiler? 'spoiler': '']">{{item.content}}</p>
            <div class="comment-nav">
                <div class="comment-nav__answere" @click="answerToggle = !answerToggle">Ответить</div>
                <div v-if="!item.spoiler" class="btn" @click="item.spoiler = !item.spoiler">Спойлер</div>
                <div v-else class="btn" @click="item.spoiler = !item.spoiler">Показать спойлер</div>
                <div class="btn" @click="report(item.id)">Пожаловаться</div>
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
        
        <div class="child-comment" v-if="item.child.length">
            <div v-if="childProp">
                <commentsItem 
                    v-for="(sub, index) in item.child" :key="index" 
                    class="sub-comments"
                    :item="sub"
                    :toggle="!deepToggle"
                />
            </div>
            
        </div>
        <div class="btn-left" v-if="!childProp && childLength" @click="allComments">Показать еще</div>
        <transition name="popup">
            <div v-if="reportState" class="report">
                <div>
                    <h1>Жалоба отправлена</h1>
                </div>
            </div>
        </transition>
    </div>
</template>

<script>
export default {
    name: 'commentsItem',
    props: {
        item: Object,
        toggle: {
            type: Boolean,
            default: true
        }
    },
    data() {
        return {
            answerToggle: false,
            answerText: '',
            reportState: false,
            childProp: true,
        }
    },
    computed: {
        deepToggle(){ 
            return this.childProp = this.toggle
        },
        activeColor(){
            return this.item.likeCounter < 0? 'red' : 'rgb(72, 235, 72)'
        },
        childLength(){
            return this.item.child.length
        }
    },
    methods: {
        allComments() {
            this.childProp = !this.childProp
        },
        sentMessage(parentName) {
            let id = Math.floor(Math.random()*10000)
            let payload = {
                id: id,
                name: `anon#${id}`,
                content: `${parentName}, ${this.answerText}`,
                likeCounter: 0,
                spoiler: false,
                child: []
            }
            this.item.child.push(payload)
            this.answerText = ''
            this.answerToggle = false
            this.childProp = true
        },
        cancelMessage() {
            this.answerText = ''
            this.answerToggle = false
        },
        setLike() {
            this.item.likeCounter ++
        },
        setDislike() {
            this.item.likeCounter --
        },
        async report(itemId){
            await new Promise(resolve => {
                setTimeout(() => {
                    resolve()
                    this.reportState = true
                }, 500)
            })
            return await new Promise(resolve => {
                setTimeout(() => {
                    resolve()
                    this.reportState = false
                }, 1000)
            })
        }
    },
    mounted(){
    }

}
</script>

<style scoped>
.sub-comments {
  margin: 0 0 0 25px;
}
.show-more {
  cursor: pointer;
}
.show-more:hover {
  opacity: .8;
}
.comment-item {
    padding: 10px 10px 10px 0;
    transition: .3s;
    border-radius: 10px;
}
.comment-item p {
    font-size: 18px;
    margin: 7px 0;
}
.comment-item:hover {
    /* background: #8080800c; */
}
.comment-item__wrap {
    display: flex;
    justify-content: space-between;
    align-items: center;
}
.comment-item__wrap h1 {
    line-height: 0.9em;
    margin: 0;
    font-size: 1.5em;
}
.comment-item__likes {
    display: flex;
}
.comment-item__likes div {
    padding: 0 10px;
    cursor: pointer;
}
.like:hover {
    color: rgb(72, 235, 72);
}
.dislike:hover {
    color: red;
}
.child-comment {
    border-left: 1px solid #80808063;
}
.comment-nav {
    display: flex;
    font-size: 0.9em;
    color: gray;
}
.comment-nav div {
    padding: 0 10px 0 0;
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
    border: 1px solid gray;
    border-radius: 10px;
    padding: 13px 13px 0 13px;
    margin: 5px 0 0 0;
    font-size: 14px;
}
.wrap-answere__text {
    height: 100px;
    margin: 0px;
    border: none;
    font-size: 18px;
    outline: none;
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
.btn-left {
    cursor: pointer;
    text-align: left;
    padding: 10px 10px 10px 0;
    color: #7f9dca;
}
.btn-left:hover {
  opacity: .8;
}
.spoiler {
    filter:blur(4px)
}
.report {
    position: fixed;
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    top: 0;
    left: 0;
}
.report div {
    width: 400px;
    height: 200px;
    border-radius: 10px;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: white;
    box-shadow: 5px 5px 12px 0 rgba(174, 174, 192, 0.4), -5px -5px 12px 0 #ffffff;
}
.popup-enter-active {
    animation: popup-in .5s;
}
.popup-leave-active {
    animation: popup-out .7s;
}
@keyframes popup-in {
    0% { transform: scale(.97); opacity: 0;}
    100% { transform: scale(1); opacity: 1;}
}
@keyframes popup-out {
    0% {transform: scale(1); opacity: 1;}
    100% { transform: scale(.97); opacity: 0;}
}
</style>