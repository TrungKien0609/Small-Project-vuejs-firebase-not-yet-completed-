<template>
  <div class="blog-container" :class="{'no-user': !user}">
    <div class="blog-content">
      <div>
        <h2 v-if="post.wellcomeScreen">{{ post.title }}</h2>
        <h2 v-else>{{ post.title }}</h2>

        <p v-if="post.wellcomeScreen">{{ post.blogPost }}</p>
        <p v-else class="content-preview">{{ post.blogHTML }}</p>

        <router-link class="link link-light" v-if="post.wellcomeScreen" to="#">
          LOGIN/REGISTER <Arrow class="arrow arrow-light" />
        </router-link>
        <router-link class="link" v-else to="#">
          VIEW THE POST <Arrow class="arrow" />
        </router-link>
      </div>
    </div>
    <div class="blog-photo">
      <img
        :src="require(`@/assets/blogPhotos/${post.photo}.jpg`)"
        v-if="post.wellcomeScreen"
        alt=""
      />
      <img
        :src="require(`@/assets/blogPhotos/${post.blogCoverPhoto}.jpg`)"
        v-else
        alt=""
      />
    </div>
  </div>
</template>
<script>
import Arrow from "@/assets/Icons/arrow-right-light.svg";
export default {
  name: "blogPost",
  components: {
    Arrow,
  },
  props: ["post"],
  computed: {
    user() {
      return this.$store.state.user;
    },
  },
};
</script>
<style lang="scss" scoped>
.blog-container {
  display: flex;
  flex-direction: column;
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1),
    0 2px 4px -1px rgba(0, 0, 0, 0.96);
  @media (min-width: 700px) {
    height: 650px;
    flex-direction: row;
  }
  .blog-content {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    flex: 4;
    order: 2;
    @media (min-width: 700px) {
      order: 1;
    }
    @media (min-width: 800px) {
      flex: 3;
    }
    div {
      max-width: 375px;
      padding: 72px 24px;
      @media (min-width: 700px) {
        padding: 0 24px;
      }
      h2 {
        font-size: 32px;
        font-weight: 300;
        text-transform: uppercase;
        margin-bottom: 24px;
        @media (min-width: 700px) {
          font-size: 40px;
        }
      }
      p {
        font-size: 15px;
        font-weight: 500;
        line-height: 1.7;
      }
      .content-preview {
        font-size: 13px;
        max-height: 24px;
        width: 250px;
        white-space: nowrap;
        overflow: hidden;
        text-overflow: ellipsis;
      }
      .link {
        display: inline-flex;
        align-items: center;
        margin-top: 32px;
        padding-bottom: 4px;
        border-bottom: 1px solid transparent;
        transition: 0.5s ease-in-out all;
        &:hover {
          border-bottom-color: #303030;
        }
      }
      .link-light {
        &:hover {
          border-bottom-color: #ffff;
        }
      }
    }
  }
  .blog-photo {
    order: 1;
    flex: 3;
    box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1),
      0 2px 4px -1px rgba(0, 0, 0, 0.06);
    @media (min-width: 700px) {
      order: 2;
    }
    @media (min-width: 800px) {
      flex: 4;
    }
    img {
      display: block;
      width: 100%;
      height: 100%;
      object-fit: cover;
    }
  }
  &:nth-child(even) {
    .blog-content {
      order: 2;
    }
    .blog-photo {
      order: 1;
    }
  }
}
.no-user:first-child {
  .blog-content {
    background-color: #303030;
    color: #fff;
  }
}
</style>