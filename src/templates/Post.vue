<template>
  <Layout>
    <!-- Page Header-->
    <header
      class="masthead"
      :style="{
        backgroundImage: `url(${GRIDSOME_API_URL + article.cover.url})`,
      }"
    >
      <div class="container position-relative px-4 px-lg-5">
        <div class="row gx-4 gx-lg-5 justify-content-center">
          <div class="col-md-10 col-lg-8 col-xl-7">
            <div class="post-heading">
              <h1>{{ article.title }}</h1>
              <h2 class="subheading">
                Problems look mighty small from 150 miles up
              </h2>
              <span class="meta">
                Posted by
                <a href="#!">Start Bootstrap</a>
                {{ article.created_at }}
              </span>
            </div>
          </div>
        </div>
      </div>
    </header>
    <!-- Post Content-->
    <article class="mb-4">
      <div class="container px-4 px-lg-5">
        <div class="row gx-4 gx-lg-5 justify-content-center">
          <div
            class="col-md-10 col-lg-8 col-xl-7"
            v-html="mdToHtml(article.content)"
          ></div>
        </div>
      </div>
    </article>
  </Layout>
</template>
<page-query>
  query($id: ID!) {
    strapiPost(id: $id) {
      id
      content
      created_at
      title
      cover {
        url
      }
      tags {
        id
        title
      }
    }
  }
</page-query>
<script>
import markDownIt from "markdown-it";
const md = new markDownIt();
export default {
  name: "PostPage",
  computed: {
    article() {
      return this.$page.strapiPost;
    },
  },
  methods: {
    mdToHtml(markdown) {
      return md.render(markdown);
    },
  },
};
</script>

<style>
</style>
