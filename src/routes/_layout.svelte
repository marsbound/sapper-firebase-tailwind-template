<script>
  import FirebaseProvider from "../components/FirebaseProvider.svelte";
  import AuthenticationProvider from "../components/AuthenticationProvider.svelte";
  import Nav from "../components/Nav.svelte";

  export let segment;
</script>

<style>
  main {
    position: relative;
    max-width: 56em;
    background-color: white;
    padding: 2em;
    margin: 0 auto;
    box-sizing: border-box;
  }
</style>

<Nav {segment} />

<main>
  <FirebaseProvider>
    <AuthenticationProvider>
      <slot />
    </AuthenticationProvider>
  </FirebaseProvider>
</main>
