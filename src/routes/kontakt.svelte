<script context="module">
  export async function load({ fetch }) {
    const res = await fetch("kontakt.json");

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
  import company from "@content/data/company.json";
  import siteData from "@content/data/site.json";
  import { browser } from "$app/env";
  import { Loader } from "@googlemaps/js-api-loader";

  export let pageDetails;

  let mapEl;
  let formEl;

  // Helper function to get form data in the supported format
  function getFormDataString(formEl) {
    var formData = new FormData(formEl),
      data = [];

    for (var keyValue of formData) {
      data.push(
        encodeURIComponent(keyValue[0]) + "=" + encodeURIComponent(keyValue[1])
      );
    }

    return data.join("&");
  }
  const handleSubmit = () => {
    var request = new XMLHttpRequest();

    request.addEventListener("load", function () {
      if (request.status === 302) {
        // CloudCannon redirects on success
        // It worked
      }
    });

    request.open(formEl.method, formEl.action);
    request.setRequestHeader(
      "Content-Type",
      "application/x-www-form-urlencoded"
    );
    console.log(getFormDataString(formEl));
    request.send(getFormDataString(formEl));
  };

  onMount(async () => {
    onCloudCannonChanges((newProps) => (pageDetails = newProps));

    if (browser) {
      const loader = new Loader({
        apiKey: siteData.google_maps_javascript_api_key,
        version: "weekly",
      });

      const google = await loader.load();
      new google.maps.Map(mapEl, {
        center: {
          lat: pageDetails.map.latitude,
          lng: pageDetails.map.longitude,
        },
        zoom: pageDetails.map.zoom,
      });
    }
    formEl = document.getElementById("contact-form");
  });

  onDestroy(async () => {
    stopCloudCannonChanges();
  });
</script>

<Page {pageDetails}>
  <section class="diagonal">
    <div class="container">
      <form
        on:submit|preventDefault={handleSubmit}
        method="post"
        action={`${siteData.baseurl}/contact-success`}
        class="contact-form"
        id="contact-form"
      >
        <input type="hidden" name="_to" value={company.contact_email_address} />
        <input type="text" name="_gotcha" />

        <div class="halves">
          <div>
            <label for="first-name">Vorname</label>
            <input
              type="text"
              name="first-name"
              id="first-name"
              placeholder="Ihr Vorname"
            />
          </div>

          <div>
            <label for="last-name">Nachname</label>
            <input
              type="text"
              name="last-name"
              id="last-name"
              placeholder="Ihr Nachname"
            />
          </div>
        </div>
        <div>
          <label for="email">E-Mail</label>
          <input
            type="text"
            name="_replyto"
            id="email"
            placeholder="Ihre-Email@Adresse.de"
            required
          />
        </div>
        <div>
          <label for="betreff">Betreff</label>
          <select name="_subject" id="betreff">
            <option>allg. Anfrage</option>
            <option>Kommentar</option>
            <option>Supportanfrage</option>
          </select>
        </div>

        <label for="message">Nachricht</label>
        <textarea name="message" id="message" placeholder="Ihre Nachricht..." />
        <input type="submit" value="Anfrage senden" />
      </form>
    </div>
  </section>
  <section class="diagonal map">
    <div id="map" bind:this={mapEl} />
  </section>

  <section class="diagonal">
    <div class="container halves aligned-top">
      <div>
        <h3>Adresse</h3>
        <address>
          <a
            target="_blank"
            href={"https://www.google.com/maps/place/" +
              encodeURIComponent(pageDetails.map.address)}
            rel="noreferrer"
          >
            {@html pageDetails.map.address.replace(/,/g, "</br>")}
          </a>
        </address>
      </div>
      <div>
        <h3>E-Mail</h3>
        <p>
          <a href={"mailto:" + company.contact_email_address}
            >{company.contact_email_address}</a
          >
        </p>
      </div>
    </div>
  </section>
</Page>

<style>
  input[name="_gotcha"] {
    display: none;
  }
</style>
