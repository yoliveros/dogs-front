<script lang="ts">
  import axios from 'axios'

  import type Dog from './Dog'

  import Input from './Input.svelte'
  import { getDogs } from './Table.svelte'
  import { URL } from './utils'

  export let isEdit = false

  export let dogState: Dog = {
    Id: '',
    Name: '',
    Owner: '',
    Breed: '',
    Age: 0
  }

  const create = () => {
    axios
      .post(URL, dogState)
      .then(() => {
        alert('New dog added')
        resetState()
      })
      .catch(err => alert(err.message))
  }

  const edit = () => {
    axios
      .patch(`${URL}/${dogState.Id}`, dogState)
      .then(() => {
        alert('Dog edited')
        resetState()
      })
      .catch(err => alert(err.message))
  }

  const resetState = () => {
    document.getElementById('close-modal').click
    dogState = {
      Id: '',
      Name: '',
      Owner: '',
      Breed: '',
      Age: 0
    }
    getDogs()
  }

  const handleSubmit = () => {
    dogState.Age = Number(dogState.Age)
    if (isEdit) {
      edit()
      return
    }

    create()
  }

  console.log(isEdit)
</script>

<form on:submit|preventDefault={handleSubmit} class="mb-10">
  <inputs class="mb-6 flex flex-col gap-4">
    <Input id="name" label="Name" bind:value={dogState.Name} required />
    <Input id="owner" label="Owner" bind:value={dogState.Owner} required />
    <Input id="age" label="Age" bind:value={dogState.Age} required />
    <Input id="breed" label="Breed" bind:value={dogState.Breed} required />
  </inputs>
  <button
    class="w-full focus:ring-4 font-medium rounded-lg text-sm px-5 py-2.5 mr-2 mb-2 bg-blue-600 hover:bg-blue-700 focus:outline-none focus:ring-blue-800"
    data-modal-hide={isEdit ? 'modal-edit' : 'modal-create'}
    type="submit"
  >
    {isEdit ? 'Edit' : 'Save'}
  </button>
</form>
