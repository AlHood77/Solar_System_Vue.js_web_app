<template lang="html">
  
<div>
    <ul>
        <li class="news-list">
            <science-news-article v-for ="(article, index) in scienceNews.articles" :article="article" :key="index"></science-news-article>
        </li>
        
    </ul>
</div>

</template>

<script>
import ScienceNewsArticle from './ScienceNewsArticle'



export default {
    name: 'science-news-list',
   
    props: ['scienceNews'],
    components: {
        "science-news-article": ScienceNewsArticle
    },

}
</script>

<style>

.news-list {
    list-style: none;
    ;
}

</style>