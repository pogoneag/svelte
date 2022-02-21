<script lang="ts">
  import {
    ListGroupItem,
    Row,
    Col,
    Card,
    CardHeader,
    CardTitle,
    CardText,
    Image,
    CardBody,
    ListGroup,
    Table,
  } from "sveltestrap";
  import { startCase } from "lodash";
  import { createEventDispatcher } from "svelte";

  export let userDetails: any = {};

  const dispatch = createEventDispatcher();
  function handleClick() {
    dispatch("closeDetails");
  }
</script>

<Card class="mb-3">
  <CardHeader>
    <Row>
      <Col><CardTitle>{userDetails.name}</CardTitle></Col>
      <Col xs="1"
        ><button
          type="button"
          class="btn-close"
          aria-label="Close"
          on:click={handleClick}
        /></Col
      >
    </Row>
  </CardHeader>
  <CardBody>
    <CardText>
      <Row>
        <Col xs="3">
          <Image
            thumbnail
            alt={userDetails.name}
            src="https://upload.wikimedia.org/wikipedia/en/2/22/Charlie_Brown.png"
          />
        </Col>
        <Col xs="9">
          <Table bordered>
            <tbody>
              {#each Object.keys(userDetails) as key}
                <tr>
                  {#if key === "address" || key === "company"}
                    <td>{startCase(key)}:</td>
                    <td>
                      <ListGroup>
                        {#each Object.keys(userDetails[key]) as addressKey}
                          <ListGroupItem color="light">
                            <strong>{startCase(addressKey)}:</strong>
                            {#if addressKey === "geo"}
                              <br />Lat : {userDetails[key][addressKey]["lat"]}
                              <br />Lng : {userDetails[key][addressKey]["lng"]}
                            {:else}
                              {userDetails[key][addressKey]}
                            {/if}
                          </ListGroupItem>
                        {/each}
                      </ListGroup>
                    </td>
                  {:else}
                    <td>{startCase(key)}:</td>
                    <td>{userDetails[key]}</td>
                  {/if}
                </tr>
              {/each}
            </tbody>
          </Table>
        </Col>
      </Row>
    </CardText>
  </CardBody>
</Card>
