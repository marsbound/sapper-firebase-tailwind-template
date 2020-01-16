<script>
  import { getContext, onMount } from "svelte";
  import { CONTEXT_KEY_FIREBASE } from "../constants";

  export let isSignedIn = false;

  const firebase = getContext(CONTEXT_KEY_FIREBASE).getFirebase();
  let email;
  let password;
  let error;
  let isLoading = false;

  const onSignInClick = () => {
    isLoading = true;
    firebase.auth
      .signInWithEmailAndPassword(email, password)
      .then(() => (isLoading = false))
      .catch(e => {
        error = e;
        isLoading = false;
      });
  };

  const onSignOutClick = () => {
    isLoading = true;
    firebase.auth
      .signOut()
      .then(() => (isLoading = false))
      .catch(e => {
        error = e;
        isLoading = false;
      });
  };
</script>

<style>
  .error-message {
    color: red;
  }
</style>

{#if isLoading}
  <p>Loading...</p>
{:else}
  <form>
    <input
      disabled={isSignedIn}
      placeholder="Email"
      type="email"
      bind:value={email} />
    <br />
    <input
      disabled={isSignedIn}
      placeholder="Password"
      type="password"
      bind:value={password} />
    <br />

    <button disabled={isSignedIn} on:click|preventDefault={onSignInClick}>
      Sign In
    </button>
    <button disabled={!isSignedIn} on:click|preventDefault={onSignOutClick}>
      Sign Out
    </button>

    {#if error}
      <p class="error-message">{error.message}</p>
    {/if}
  </form>
{/if}
