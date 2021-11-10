<script context="module">
  export async function load({ fetch }) {
    const res = await fetch("index.json");

    if (res.ok) {
      return {
        props: res.json(),
      };
    }
  }
</script>

<script>
  import { onDestroy, onMount } from "svelte";
  import {
    onCloudCannonChanges,
    stopCloudCannonChanges,
  } from "@cloudcannon/svelte-connector";

  import Page from "$lib/components/Page.svelte";
  import siteData from "@content/data/site.json";
  export let pageDetails;
  export let clients;

  onMount(async () => {
    onCloudCannonChanges((newProps) => (pageDetails = newProps));
  });
  onDestroy(async () => {
    stopCloudCannonChanges();
  });

  let clientsPreview = clients.slice(0, 4);
</script>

<Page {pageDetails} withContactButton="true">
  <section class="diagonal patterned">
    <div class="container halves">
      <div>
        <h3>{pageDetails.portfolio_heading}</h3>
        <p>{@html pageDetails.portfolio_description_html}</p>

        <p>
          <a href={`${siteData.baseurl}/referenzen`}
            >{pageDetails.portfolio_call_to_action} &rarr;</a
          >
        </p>
      </div>
      <div>
        <ul class="image-grid">
          {#each clientsPreview as client, index (index)}
            <li>
              <a href={`${siteData.baseurl}/clients/${client.slug}`}>
                <img src={client.image_path} alt={client.name} />
              </a>
            </li>
          {/each}
        </ul>
      </div>
    </div>
  </section>

  <section class="diagonal alternate">
    <div class="container halves">
      <div>
        <ul class="image-list">
          <li>
            <img
              src="/images/netlify_logomark.svg"
              width="125"
              class="netlify-logo"
              alt="Netlify Logo"
            />
          </li>
          <li>
            <img
              src="/images/cloudcannon-logo-blue.svg"
              width="175"
              class="cloudcannon-logo"
              alt="CloudCannon Logo"
            />
          </li>
          <li>
            <img
              src="/images/stackbit-monogram.svg"
              width="125"
              class="stackbit-logo"
              alt="Stackbit Logo"
            />
          </li>
          <li>
            <img src="/images/svelte-logo.svg" width="120" alt="Jekyll Logo" />
          </li>
          <li>
            <img
              src="/images/Octocat.png"
              width="200"
              class="github-logo"
              alt="GitHub Logo"
            />
          </li>
        </ul>
      </div>
      <div>
        <h3>Neueste Software, beste Perfomance</h3>
        <p>
          Als junge Agentur können wir uns ganz auf die neuesten und
          performantesten Technologien fokussieren. Entdecken auch Sie die
          Vorteile einer schlanken, modularen Architektur und machen Sie
          Cloud-Editing zu einem Kreativ-Erlebnis.
        </p>
      </div>
    </div>
  </section>
</Page>
