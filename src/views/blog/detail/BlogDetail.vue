<template>
    <ps-content-container class="sm:mt-32 lg:mt-36 mt-28 mb-16">
        <template #content>
            <div class="flex flex-col">
                
                <div class="flex items-center "> 
                    <ps-route-link
                    textSize="text-lg sm:text-xl lg:text-2xl"
                        class="hover:underline cursor-pointer font-medium"
                        :to="{name: 'blog-list' }"> 
                            {{ $t("blog_detail__blog_list") }}
                    </ps-route-link>
                </div>

                <div class=" w-auto cursor-pointer my-2 mb-16 ">
                    <img alt="Placeholder" width="300px" height="200px" class="block w-full rounded-xl lg:rounded-2xl lg:h-96 h-56 sm:h-72  object-cover" :src="blogProvider.imageUrl( blogProvider.blog?.data?.defaultPhoto?.imgPath )" @error="blogProvider.defaultCarImage">
                    <div class="mt-4">
                        <ps-label-title> {{blogProvider.blog?.data?.name}} </ps-label-title>
                        <p class="mt-4" v-if="blogProvider.blog.data != null">
                            <ps-label v-html="blogProvider.blog.data.description"> </ps-label>
                        </p>
                    </div>
                </div>
                <!-- google adsense desktop view -->
                <div class="hidden md:block">
                    <ps-ad-sense class=" sm:w-median lg:w-large" adFormat="horizontal"></ps-ad-sense>
                </div>

            </div>
        </template>
    </ps-content-container>
</template>

<script lang="ts">
//Vue
import { useRoute } from 'vue-router';

import PsContentContainer from "@/components/layouts/container/PsContentContainer.vue";
import PsRouteLink from '@/components/core/link/PsRouteLink.vue';
import PsLabelTitle from '@/components/core/label/PsLabelTitle.vue';
import PsLabel from '@/components/core/label/PsLabel.vue';
import PsAdSense from '@/components/core/adsense/PsAdSense.vue';

//Models
import { createBlogProviderState } from '@/store/modules/blog/BlogProvider';
import PsConst from '@/object/constant/ps_constants';

export default {
    name : "BlogDetailView",
    components : {
        PsContentContainer,
        PsRouteLink,
        PsLabelTitle,
        PsLabel,
        PsAdSense
    },
    setup() {
        const route = useRoute();
        const blogId = route.params.blogId.toString();
        // Inject Provider
        const blogProvider = createBlogProviderState();

        blogProvider.loadBlog(blogId,PsConst.NO_LOGIN_USER);
        
        return {
            blogProvider
        }
    }
}
</script>