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
    Age: 0
  }

  const handleSubmit = () => {
    axios
      .post(URL, newDog)
      .then(() => {
        alert('New dog added')
        document.getElementById('close-modal').click
        newDog = {
          Id: '',
          Name: '',
          Owner: '',
          Breed: '',
          Age: 0
        }
      })
      .catch(err => alert(err.message))
  }
</script>

<form on:submit|preventDefault={handleSubmit} class="mb-10">
  <inputs class="mb-6 flex flex-col gap-4">
    <Input id="name" label="Name" bind:value={newDog.Name} required />
    <Input id="owner" label="Owner" bind:value={newDog.Owner} required />
    <Input id="age" label="Age" bind:value={newDog.Age} required />
    <Input id="breed" label="Breed" bind:value={newDog.Breed} required />
  </inputs>
  <button
    class="w-full focus:ring-4 font-medium rounded-lg text-sm px-5 py-2.5 mr-2 mb-2 bg-blue-600 hover:bg-blue-700 focus:outline-none focus:ring-blue-800"
    data-modal-hide="dogs-modal"
    type="submit"
  >
    Add
  </button>
</form>
