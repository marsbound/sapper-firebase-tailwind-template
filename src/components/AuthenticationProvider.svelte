<script>
  import { onDestroy, setContext, getContext } from "svelte";
  import { readable } from "svelte/store";

  import { CONTEXT_KEY_FIREBASE, CONTEXT_KEY_CURRENT_USER } from "../constants";

  let listener;
  const firebase = getContext(CONTEXT_KEY_FIREBASE).getFirebase();

  const currentUser = readable(null, set => {
    listener = firebase.auth.onAuthStateChanged(user => {
      user ? set(user) : set(null);
    });
  });

  setContext(CONTEXT_KEY_CURRENT_USER, currentUser);

  onDestroy(() => {
    listener();
  });
</script>

<slot />
