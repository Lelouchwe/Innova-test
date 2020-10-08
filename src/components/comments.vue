<template>
  <div class="container">
        <commentsItem 
            v-for="(item, index) in comments" :key="index"
            :item="item"
        />
        <div class="show-more">
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
      comments: [
        {
          id: 1,
          name: 'john',
          content: 'something text here',
          child: [
            {
              id: 12,
              name: 'john',
              content: 'something text here',
              child: [
                {
                id: 12,
                name: 'john',
                content: 'something text here'
                },
                {
                id: 13,
                name: 'john',
                content: 'something text here'
                },
            ]
            },
            {
              id: 13,
              name: 'john',
              content: 'something text here'
            },
          ]
        },
        {
          id: 2,
          name: 'wick',
          content: 'something text here'
        },
        {
          id: 3,
          name: 'ger',
          content: 'something text here'
        },
      ],
    }
  },
  methods: {

  },
  mounted() {
      console.log(commentsJson);
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