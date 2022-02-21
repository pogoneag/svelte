<script lang="ts">
  import { Col, Container, Row } from "sveltestrap";
  import { onMount } from "svelte";
  import List from "./lib/List.svelte";
  import Details from "./lib/Details.svelte";

  const USERS_URL = "https://jsonplaceholder.typicode.com/users";
  let users = [];
  let userDetails;
  let showDetails = false;

  onMount(async () => {
    fetch(USERS_URL)
      .then((response) => response.json())
      .then((data) => {
        showDetails = false;
        users = data;
      })
      .catch((error) => {
        console.log(error);
        return [];
      });
  });

  function handleUserDetails({ detail }) {
    fetch(`${USERS_URL}/${detail.id}`)
      .then((response) => response.json())
      .then((data) => {
        userDetails = data;
        showDetails = true;
      });
  }
</script>

<Container>
  <Row>
    <Col xs="2" />
    <Col xs="8">
      {#if !showDetails}
        <List {users} on:viewDetails={handleUserDetails} />
      {:else}
        <Details {userDetails} on:closeDetails={() => (showDetails = false)} />
      {/if}
    </Col>
    <Col xs="2" />
  </Row>
</Container>
