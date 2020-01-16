<script>
  import { getContext } from "svelte";
  import SignInForm from "../components/SignInForm.svelte";
  import { CONTEXT_KEY_CURRENT_USER } from "../constants";

  const currentUser = getContext(CONTEXT_KEY_CURRENT_USER);
</script>

<svelte:head>
  <title>Auth</title>
</svelte:head>

<h1>You're signed in as...</h1>

{#if $currentUser}
  <p>{$currentUser.email}</p>
{/if}

<SignInForm isSignedIn={$currentUser} />
