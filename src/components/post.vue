<style>

.sidebar {
    box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
    text-align: center;
    padding: 1%;

}

</style>

<template>


    <transition name="slide-fade">


        <div class="container" v-if="loaded === 'true'">
            <section class="hero is-primary is-medium">
                <div class="hero-body">

                    <!--<div class="progressive">-->
                    <!--post.better_featured_image.media_details.sizes.medium-->
                        <!--<img class="preview" v-progressive="post.featured_image_src['full'][0]"-->
                             <!--:data-srcset="post.featured_image_src['srcset']"-->
                             <!--:src="post.featured_image_src['full'][0]"/>-->

                    <!--</div>-->
                    <div class="container has-text-centered">
                        <h1 class="title is-2">
                            {{ post.title.rendered }}
                        </h1>
                        <h2 class="subtitle is-4">
                            <span class="posted-on">
							Posted On
							<span class="date" v-text="formatDate( post )">
							</span>
						</span>
                        </h2>
                    </div>
                </div>
            </section>

                    <!--<div class="progressive">-->

                        <!--<img class="preview" v-progressive="post.featured_image_src['full'][0]"-->
                             <!--:data-srcset="post.featured_image_src['srcset']"-->
                             <!--:src="post.featured_image_src['full'][0]"/>-->

                    <!--</div>-->

                    <div class="rt-post-content rt-content" v-html="post.content.rendered"></div>

                </div>



            <!--Sidebar-->
            <!--<div class="medium-3 columns">-->

                <!--<div class="sidebar" style="width: 300px;">-->
                    <!--<div class="card-section">-->
                        <!--<h4>This is a card.</h4>-->
                        <!--<p>It has an easy to override visual style, and is appropriately subdued.</p>-->
                    <!--</div>-->
                <!--</div>-->

            <!--</div>-->


    </transition>

</template>

<script>
    export default {

        mounted: function () {

            this.getPost();
        },

        data() {
            return {
                base_path: rtwp.base_path,
                post: {},
                loaded: 'false',
                pageTitle: ''

            }
        },

        methods: {
            getPost: function () {

                var vm = this;

                vm.$http.get('wp/v2/posts', {
                    params: {slug: vm.$route.params.name}
                })
                    .then((res) => {

                        vm.post = res.data[0];
                        vm.loaded = 'true';
                        vm.pageTitle = vm.post.title.rendered;
                        vm.$store.commit('rtChangeTitle', vm.pageTitle);
//                        vm.image = vm.post.featured_media;
                        console.log(vm.pageTitle)
                    })
                    .catch((res) => {
                        console(`Something went wrong : ${res}`);
                    })


            },
            formatDate: function (value) {
                value = value.date;
                if (value) {
                    var date = new Date(value);
                    var monthNames = ["January", "February", "March",
                        "April", "May", "June", "July",
                        "August", "September", "October",
                        "November", "December"
                    ];

                    var day = date.getDate();
                    var monthIndex = date.getMonth();
                    var year = date.getFullYear();

                    return monthNames[monthIndex] + ',' + day + ' ' + year;
                }

            },
            getBlogImage: function () {

            }
        }
    }
</script>