<script context="module">
  export function load({ error, status }) {
    return {
      props: {
        message: error.message,
        status: status,
      },
    };
  }
</script>

<script>
  import Page from "$lib/components/Page.svelte";
</script>

<Page pageDetails={{ title: "Nicht gefunden" }}>
  <section class="diagonal">
    <div class="container">
      <p>Die angeforderte Seite kann leider nicht geladen werden.</p>
    </div>
  </section>
</Page>
