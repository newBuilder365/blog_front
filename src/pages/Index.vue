<template>
  <Layout>
    <!-- Page Header-->
    <header
      class="masthead"
      :style="{
        backgroundImage: `url(${GRIDSOME_API_URL + general.cover.url})`,
      }"
    >
      <div class="container position-relative px-4 px-lg-5">
        <div class="row gx-4 gx-lg-5 justify-content-center">
          <div class="col-md-10 col-lg-8 col-xl-7">
            <div class="site-heading">
              <h1>{{ general.title }}</h1>
              <span class="subheading">{{ general.subtitle }}</span>
            </div>
          </div>
        </div>
      </div>
    </header>
    <!-- Main Content-->
    <div class="container px-4 px-lg-5">
      <div class="row gx-4 gx-lg-5 justify-content-center">
        <div class="col-md-10 col-lg-8 col-xl-7">
          <!-- Post preview-->
          <div class="post-preview" v-for="post in posts" :key="post.id">
            <a href="post.html">
              <h2 class="post-title">
                <g-link :to="'/post/' + post.node.id">
                  {{ post.node.title }}
                </g-link>
              </h2>
              <!-- <h3 class="post-subtitle">
                post by
                {{
                  `${post.node.created_by.firstname}${post.node.created_by.lastname}`
                }}
                at {{ post.node.created_at }}
              </h3> -->
            </a>
            <p class="post-meta">
              <span v-for="tag in post.node.tags" :key="tag.id">
                <g-link :to="'/tag/' + tag.id">
                  {{ tag.title }}
                </g-link>
                &nbsp;&nbsp;
              </span>
            </p>
            <hr class="my-4" />
          </div>
          <!-- Divider-->
          <!-- Pager-->
          <div class="d-flex justify-content-end mb-4">
            <!-- <a class="btn btn-primary text-uppercase" href="#!"
              >Older Posts →</a
            > -->
            <Pager :info="$page.posts.pageInfo" />
          </div>
        </div>
      </div>
    </div>
  </Layout>
</template>
<page-query>
  query($page:Int) {
    posts: allStrapiPost(perPage:2, page:$page) @paginate{
      pageInfo {
      totalPages
      currentPage
    }
      edges {
        node {
          id
          title
          created_at
          tags {
            id
            title
          }
        }
      }
    }
    allStrapiGeneral {
     edges {
       node {
         title
         subtitle
         cover {
           url
         }
       }
     }
    }
  }
</page-query>
<script>
import { Pager } from "gridsome";
export default {
  name: "Home",
  metaInfo: {
    title: "Hello, world!",
  },
  computed: {
    posts() {
      return this.$page.posts.edges;
    },
    general() {
      return this.$page.allStrapiGeneral.edges[0].node;
    },
  },
  components: {
    Pager,
  },
};
</script>

<style></style>
