<script lang="ts">
  import { GetNewsArticles } from "$lib/apis/newsapi";
  import type { article } from "$lib/types";
  import { onMount } from "svelte";

  let articles: article[] = [];
  let keyword: string = "bitcoin";

  async function getArticles() {
    articles = await GetNewsArticles(keyword);

    console.log(articles);
  }
</script>

<h1>Welcome to SvelteKit</h1>
<p>
  Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation
</p>

<input type="text" bind:value={keyword} />
<button on:click={getArticles}>Search</button>

<h2>News Articles</h2>
<ul>
  {#each articles as article}
    <li>
      <img src={article.urlToImage} alt={article.title} />
      <a href={article.url}>
        {article.title} - {article.publishedAt}
      </a>
    </li>
  {/each}
</ul>
