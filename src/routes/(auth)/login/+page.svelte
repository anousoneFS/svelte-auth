<script lang="ts">
	import { applyAction, enhance } from '$app/forms'
	import { invalidateAll } from '$app/navigation'
	/* import { enhance } from '$app/forms' */
  import type { ActionData } from './$types'
	export let form: ActionData;
</script>

<h1>Login</h1>
<!-- <form action="?/login" method="POST" use:enhance> -->
<form action="?/login" method="POST" use:enhance = {() => {
  return async({result}) => {
     // rerun the `load` function for the page
			// https://kit.svelte.dev/docs/modules#$app-navigation-invalidateall
			invalidateAll()

			// since we're customizing the default behaviour
			// we don't want to reimplement what `use:enhance` does
			// so we can use `applyAction` and pass the `result`
			await applyAction(result)
  }
}}>
	<div>
		<label for="username">Username</label>
		<input type="text" id="username" name="username" required />
	</div>
	<div>
		<label for="password">Password</label>
		<input type="text" id="password" name="password" required />
	</div>
  {#if form?.invalid}
    <p class="error">Username and password is required</p>
  {/if}
  {#if form?.credentials}
    <p class="error">You have enter the wrong credentials</p>
  {/if}
    <button type="submit">Login</button>
</form>
