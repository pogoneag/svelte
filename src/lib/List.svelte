<script lang="ts">
  import { Habitats } from "../enums/habitats";
  import { Table } from "sveltestrap";
  import type { AnimalsModel } from "@/models/Animals";
  export let animals: AnimalsModel[] = [];
  export let habitat: Habitats = Habitats.ALL;
  $: filterItems = animals.filter(
    (item: any) => item.life_habitat === habitat || habitat === Habitats.ALL
  );
</script>

<Table>
  <thead>
    <tr>
      <th>#</th>
      <th>Animal</th>
    </tr>
  </thead>
  <tbody>
    {#each filterItems as animal, i}
      <tr>
        <th scope="row">{i + 1}</th>
        <td>{animal.name}</td>
      </tr>
    {/each}
  </tbody>
</Table>
