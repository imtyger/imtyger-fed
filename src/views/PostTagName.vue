<template>
    <div class="content">
      <span><h2>{{ tagName }}</h2></span>
      <!--<span v-if="blogList !== null && blogList.size !== 0">-->
        <h4>
          <div v-for="blog in blogList">
            <span>{{ blog.createdAt | formatDate }}</span>
            <span> -- </span>
            <router-link :to="{path:'/post/'+ blog.id }">
              <span>{{ blog.title }}</span>
            </router-link>
          </div>
        </h4>
      <!--</span>-->

    </div>
</template>

<script>
  import { getBlogsPostTagName } from '../api/blog'
  export default {
    data () {
      return {
        tagName: this.$route.params.tagName,
        blogList: {}
      }
    },
    mounted () {
      this.getBlogList()
    },
    watch: {
      $route(to, from) {
        this.getBlogList()
      }
    },
    methods:{
      async getBlogList(){
        const data = await getBlogsPostTagName(this.tagName);
        this._formatList(data)
      },
      _formatList(data) {
        this.blogList = data.data;
      },
    }
  }
</script>

<style scoped>

  h3,h4,h5{
    font-weight: normal;
    font-size: 16px;
  }

  .content {
    margin: 10px 180px 10px 180px;
    padding: 20px;
  }
</style>
