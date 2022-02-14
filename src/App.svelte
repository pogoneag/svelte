<script lang="ts">
  import { Col, Container, Row, FormGroup, Label, Input } from "sveltestrap";
  import { Habitats } from "./enums/habitats";
  import List from "./lib/List.svelte";
  import type { AnimalsModel } from "./models/Animals";

  const animals: AnimalsModel[] = [
    {
      name: "Dog",
      life_habitat: Habitats.TERRESTRIAL,
    },
    {
      name: "Whale",
      life_habitat: Habitats.AQUATIC,
    },
    {
      name: "Cat",
      life_habitat: Habitats.TERRESTRIAL,
    },
    {
      name: "Bee",
      life_habitat: Habitats.AIR,
    },
  ];
  let habitat = Habitats.ALL;
</script>

<Container>
  <Row>
    <Col xs="3" />
    <Col xs="6">
      <FormGroup>
        <Label for="habitats">Habitats</Label>
        <Input type="select" bind:value={habitat} name="habitats" id="habitats">
          <option value={Habitats.ALL} selected>All</option>
          <option value={Habitats.TERRESTRIAL}>Terrestrial</option>
          <option value={Habitats.AQUATIC}>Aquatic</option>
          <option value={Habitats.AIR}>Air</option>
        </Input>
      </FormGroup>
    </Col>
    <Col xs="3" />
  </Row>
  <Row>
    <Col xs="3" />
    <Col xs="6">
      <List {animals} {habitat} />
    </Col>
    <Col xs="3" />
  </Row>
</Container>
