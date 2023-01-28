<script lang="ts">
  import axios from 'axios'

  import type Dog from './Dog'

  import Input from './Input.svelte'
  import { URL } from './utils'

  let newDog: Dog = {
    Id: '',
    Name: '',
    Owner: '',
    Breed: '',
    Age: ''
  }

  const handleSubmit = () => {
    axios.post(URL).then(response => console.log(response))
  }
</script>

<form on:submit|preventDefault={handleSubmit} class="mb-10">
  <inputs class="grid gap-4 mb-6 md:grid-cols-2">
    <Input id="name" label="Name" bind:value={newDog.Name} />
    <Input id="owner" label="Owner" bind:value={newDog.Owner} />
    <Input id="age" label="Age" bind:value={newDog.Age} />
    <Input id="breed" label="Breed" bind:value={newDog.Breed} />
  </inputs>
  <button class="bg-sky-800 h-10 w-1/4" type="submit">Add</button>
</form>
