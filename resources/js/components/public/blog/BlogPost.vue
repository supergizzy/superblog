<template>
    <span id="blogpost">
        <section id="inner-headline">
            <div class="container">
                <div class="row">
                <div class="span4">
                    <div class="inner-heading">
                    <h2>Blog left sidebar</h2>
                    </div>
                </div>
                <div class="span8">
                    <ul class="breadcrumb">
                    <li><a href="#"><i class="icon-home"></i></a><i class="icon-angle-right"></i></li>
                    <li><a href="#">Blog</a><i class="icon-angle-right"></i></li>
                    <li class="active">Blog with left sidebar</li>
                    </ul>
                </div>
                </div>
            </div>
        </section>
        <section id="content">
            <div class="container">
                <div class="row">
                <div class="span8">
                    <article v-for="post in blogpost" :key="post.id">
                        <div class="row">
                            <div class="span8">
                            <div class="post-image">
                                <div class="post-heading">
                                <h3><a href="#">{{post.title}}</a></h3>
                                </div>
                                <img :src="`uploadimage/${post.photo}`" alt="" class="img-fluid"/>
                            </div>
                            <p>{{post.description | sortlength(300,".....")}}</p>
                            <div class="bottom-article">
                                <ul class="meta-post">
                                <li><i class="icon-calendar"></i><a href="#">{{ post.created_at | timeformat }}</a></li>
                                <li v-if="post.user">
                                    <i class="icon-user"></i><a href="#">{{ post.user.name }}</a>
                                </li>
                                <li v-if="post.category">
                                    <i class="icon-folder-open"></i><a href="#">{{ post.category.cat_name }}</a>
                                </li>
                                <li><i class="icon-comments"></i><a href="#">4 Comments</a></li>
                                </ul>
                                <a href="#" class="pull-right">Continue reading <i class="icon-angle-right"></i></a>
                            </div>
                            </div>
                        </div>
                    </article>
                    <div id="pagination">
                    <span class="all">Page 1 of 3</span>
                    <span class="current">1</span>
                    <a href="#" class="inactive">2</a>
                    <a href="#" class="inactive">3</a>
                    </div>
                </div>
                <BlogSidebar/>
                </div>
            </div>
        </section>
    </span>
</template>

<script>
import BlogSidebar from './BlogSidebar.vue'
export default {
    name: "BlogPost",
    components: {
        BlogSidebar
    },
    mounted(){
        this.$store.dispatch("getBlogPost")
    },
    computed:{
        blogpost(){
            return this.$store.getters.getBlogPost
        }
    },
    methods:{

    }
}
</script>

<style scoped>
.post-image img {
    height: auto;
    width: 70%;
}
</style>