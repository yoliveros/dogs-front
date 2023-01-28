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

<table class="w-full text-sm text-left  text-gray-400">
  <thead class="text-xs uppercase bg-gray-700 text-gray-400">
    <tr>
      <th scope="col" class="px-6 py-3">Name</th>
      <th scope="col" class="px-6 py-3">Owner</th>
      <th scope="col" class="px-6 py-3">Age</th>
      <th scope="col" class="px-6 py-3">Breed</th>
      <th scope="col" class="px-6 py-3">Actions</th>
    </tr>
  </thead>
  <tbody>
    {#each dogsArray as dog}
      <tr class="border-b bg-gray-800 border-gray-700">
        <td class="px-6 py-4">{dog.Name}</td>
        <td class="px-6 py-4">{dog.Owner}</td>
        <td class="px-6 py-4">{dog.Age}</td>
        <td class="px-6 py-4">{dog.Breed}</td>
        <td class="px-6 py-4"> X </td>
      </tr>
    {/each}
  </tbody>
</table>
