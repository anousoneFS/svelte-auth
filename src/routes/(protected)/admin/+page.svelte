<script lang="ts">
  import { page } from '$app/stores'
</script>

  <h1>Admin</h1>

{#if $page.data.user} 
  <p>Hello {$page.data.user.name} !</p>
{/if}

{#if $page.data.user.role === 'USER'}
  <form action="/logout" method='POST'>
    <button type='submit'>Log out</button>
  </form>
{/if}

