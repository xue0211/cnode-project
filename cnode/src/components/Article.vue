<template>
    <div class="article">
        <!-- 如果正在加载数据，显示此 div -->
        <div class="loading" v-if="isLoading"> <!--加载动画-->
            <img src="../assets/loading.gif">
        </div>
        <div v-else>
            <div class="topic_header">
                <div class="topic_title">{{ post.title }}</div>
                <ul>
                    <li>·发布于:{{ post.create_at | formatDate }}</li> <!-- formatDate 过滤器-->
                    <li>·作者：
                        {{ post.author.loginname }}
                    </li>
                    <li>·{{ post.visit_count }}次浏览</li>
                    <li>·来自{{ post | tabFormatter }} </li> <!--tabFormatter 过滤器-->
                </ul>
                <div v-html="post.content" class="topic_content"></div>
            </div>
            <div>
                <div class="topbar">回复</div>
                <div v-for="(reply, index) in post.replies" class="replySec">
                    <div class="replyUp">
                        <router-link>
                            <img :src="reply.author.avatar_url" alt=""> <!--头像-->
                        </router-link>
                        <router-link>
                            <span>{{ reply.author.loginname }}</span> <!--用户名-->
                        </router-link>
                        <span>
                            #{{ index + 1 }}楼
                        </span>
                        <span v-if="reply.ups.length > 0">
                            ☝ {{ reply.ups.length }}
                        </span>
                        <span v-else>
                        </span>
                        <p v-html="reply.content"></p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Article',
    data() {
        return {
            isLoading: false, // 动画是否加载
            post: {} // 代表当然文章页的所有内容、所有属性
        }
    },
    methods: {
        getArticleData() {
            this.$http.get(`https://cnodejs.org/api/v1/topic/${this.$route.params.id}`)
                .then(res => {
                    if (res.data.success == true) {
                        this.isLoading = false
                        this.post = res.data.data
                    }
                })
                .catch(function (err) {
                    console.log(err)
                })
        }
    },
    beforeMount() {
        this.isLoading = true
        this.getArticleData()
    }
}
</script>

<style>
@import url('../assets/markdown-github.css');
</style>