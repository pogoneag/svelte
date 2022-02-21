<script lang="ts">
  import { Button, Table } from "sveltestrap";
  import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

  export let users = [];
  function handleClick(id: string) {
    dispatch('viewDetails', { id });
  }
</script>

<Table>
  <thead>
    <tr>
      <th>#</th>
      <th>Name</th>
      <th>Email</th>
      <th>Phone</th>
      <th>Actions</th>
    </tr>
  </thead>
  <tbody>
    {#each users as user, i}
      <tr>
        <th scope="row">{i + 1}</th>
        <td>{user.name}</td>
        <td>{user.email}</td>
        <td>{user.phone}</td>
        <td>
          <Button outline color="primary" on:click={() => handleClick(user.id)}>View</Button>
        </td>
      </tr>
    {/each}
  </tbody>
</Table>
