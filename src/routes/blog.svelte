<script context="module">
  export async function load({ fetch }) {
    const url = "blog.json";
    const res = await fetch(url);

    if (res.ok) {
      return {
        props: res.json(),
      };
    }
  }
</script>

<script>
  import Page from "$lib/components/Page.svelte";
  import PostSummary from "$lib/components/PostSummary.svelte";

  export let posts, pageDetails;
</script>

<Page {pageDetails}>
  <section class="diagonal">
    <div class="text-container">
      <p class="editor-link">
        <a href="cloudcannon:collections/content/posts" class="btn"
          ><strong>&#9998;</strong> Beitrag hinzufügen</a
        >
      </p>
      <ul class="blog-posts">
        {#each posts as post, index (index)}
          <li class="blog-post">
            <PostSummary {post} />
          </li>
        {/each}
      </ul>
    </div>
  </section>
</Page>
