<template>
  <div class="home">
    <BlogPost v-if="!user" :post="wellcomeScreen" />
    <BlogPost
      v-for="(post, index) in sampleBlogPost"
      :key="index"
      :post="post"
    />
    <div class="blog-card-wrap">
      <div class="container">
        <h3>View mor recent Blogs</h3>
        <div class="blog-cards">
          <BlogCard
            :post="card"
            v-for="(card, index) in sampleBlogCards"
            :key="index"
          />
        </div>
      </div>
    </div>
    <div class="updates" v-if="!user">
      <div class="container">
        <h2>never miss a post. Register for free accout today!</h2>
        <router-link class="router-button" to="#">
          Register for FireBlogs <Arrow class="arrow arrow-light" />
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import BlogPost from "../components/BlogPost.vue";
import BlogCard from "../components/BlogCard.vue"
import Arrow from "@/assets/Icons/arrow-right-light.svg";
import {mapState} from 'vuex'
export default {
  name: "Home",
  components: {
    BlogPost,
    BlogCard,
    Arrow
  },
  data() {
    return {
      wellcomeScreen: {
        title: "Welcome",
        blogPost:
          "Weekly blog articles with all things programming including HTML, CSS, JavaScript and more. Register today to never miss a post!",
        wellcomeScreen: true,
        photo: "coding",
      },
      sampleBlogPost: [
        {
          title: "This is Filter Titile",
          blogHTML: "This is a fillter blog post title",
          blogCoverPhoto: "beautiful-stories",
        },
        {
          title: "This is Filter Titile",
          blogHTML: "This is a fillter blog post title",
          blogCoverPhoto: "designed-for-everyone",
        },
      ],
    };
  },
  computed:{
    ...mapState(["sampleBlogCards"]),
    // sampleBlogCards(){
    //   return this.$store.state.sampleBlogCards
    // }
    user(){
      return this.$store.state.user ;
  }
  }
};
</script>
<style lang="scss" scoped>
.blog-card-wrap {
  h3 {
    font-weight: 300;
    font-size: 28px;
    margin-bottom: 32px;
  }
}
.updates {
  .container {
    padding: 100px 25px;
    display: flex;
    flex-direction: column;
    align-items: center;
    @media (min-width: 800px) {
      padding: 125px 25px;
      flex-direction: row;
    }
    .router-button {
      display: flex;
      font-size: 14px;
      text-decoration: none;
      @media (min-width: 800px) {
        margin-left: auto;
      }
    }
    h2 {
      font-size: 32px;
      max-width: 425px;
      width: 100%;
      text-align: center;
      text-transform: uppercase;
      font-weight: 300;
      @media (min-width: 800px) {
        text-align: initial;
        font-size: 40px;
      }
    }
  }
}
</style>
