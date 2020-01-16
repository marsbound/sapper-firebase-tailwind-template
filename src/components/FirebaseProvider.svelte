<script>
  import app from "firebase/app";
  import "firebase/auth";
  import "firebase/firestore";
  import { onMount, setContext } from "svelte";
  import { CONTEXT_KEY_FIREBASE } from "../constants";

  setContext(CONTEXT_KEY_FIREBASE, {
    getFirebase: () => firebase
  });

  let firebase;

  onMount(() => {
    const configs = {
      apiKey: "FIREBASE_API_KEY",
      authDomain: "FIREBASE_AUTH_DOMAIN",
      databaseURL: "FIREBASE_DATABASE_URL",
      projectId: "FIREBASE_PROJECT_ID",
      storageBucket: "FIREBASE_STORAGE_BUCKET",
      messagingSenderId: "FIREBASE_MESSAGING_SENDER_ID",
      appId: "FIREBASE_APP_ID"
    };

    app.initializeApp(configs);
    const auth = app.auth();
    const db = app.firestore();
    firebase = { auth, db };
  });
</script>

{#if firebase}
  <slot />
{:else}
  <h1>Loading Firebase...</h1>
{/if}
