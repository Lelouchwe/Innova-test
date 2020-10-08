<template>
  <div class="container">
        <h1>На фоне отсутствия блокбастеров «Бегущий по лезвию» стартовал с первой строчки проката РФ</h1>
        <img src="https://leonardo.osnova.io/04190036-ae5a-5454-929a-58dd0cc2b37e/-/resize/1400/" alt="">
        <p style="line-height: 1.9em;">Культовый фильм Ридли Скотта «Бегущий по лезвию» вышел в повторный российский прокат 8 октября. 
          По данным системы ЕАИС, только за ночь и на предпродажах к релизу он собрал 877 тысяч рублей.
          По сборам за ночь «Бегущему по лезвию» удалось более чем в два раза обойти «Стрельцова», 
          вышедшего ранее 24 сентября, и «Довод». Вероятно, сборы за первый день проката также будут больше, 
          однако до какого уровня они доберутся, сказать сложно. Ситуация может и измениться.
        </p>
        <div class="comments">
          <h1>Комментарии</h1>
          <comments/>
        </div>
  </div>
</template>

<script>
export default {
    components: {
        comments: () => import('@/components/comments.vue')
    }
}
</script>

<style scoped>
  .container {
    width: 50vw;
    margin: 0 auto;
  }
  h1, p {
    text-align: left;
  }
  img {
    width: 100%;
  }
  .comments {
    margin: 50px 0;
  }
  
</style>