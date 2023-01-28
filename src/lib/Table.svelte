<script lang="ts">
  import { onMount } from 'svelte'
  import axios from 'axios'
  import type Dog from './Dog'
  const URL = 'http://localhost:3000/dogs'
  let dogsArray: Dog[] = []

  onMount(() => {
    axios.get<Dog[]>(URL).then(({ data }) => {
      dogsArray = data
    })
  })
</script>

<table class="w-full">
  <thead>
    <tr>
      <th>Name</th>
      <th>Owner</th>
      <th>Age</th>
      <th>Breed</th>
    </tr>
  </thead>
  <tbody>
    {#each dogsArray as dog}
      <tr>
        <td>{dog.Name}</td>
        <td>{dog.Owner}</td>
        <td>{dog.Age}</td>
        <td>{dog.Breed}</td>
      </tr>
    {/each}
  </tbody>
</table>
