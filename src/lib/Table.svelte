<script context="module" lang="ts">
  import { writable } from 'svelte/store'
  let dogsArray = writable<Dog[]>([])
  export const getDogs = () => {
    axios.get<Dog[]>(URL).then(({ data }) => {
      dogsArray.set(data)
    })
  }
</script>

<script lang="ts">
  import { onMount } from 'svelte'
  import axios from 'axios'
  import { URL } from './utils'
  import type Dog from './Dog'
  import Modal from './Modal.svelte'
  import Form from './Form.svelte'

  let setDog: Dog = {
    Id: '',
    Name: '',
    Owner: '',
    Breed: '',
    Age: 0
  }

  onMount(() => {
    getDogs()
  })

  const handleEdit = (dog: Dog) => {
    setDog = dog
  }

  const handleDelete = (id: string) => {
    axios.delete(`${URL}/${id}`).then(() => {
      getDogs()
      alert('Dog deleted')
    })
  }
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
    {#each $dogsArray as dog}
      <tr class="border-b bg-gray-800 border-gray-700">
        <td class="px-6 py-4">{dog.Name}</td>
        <td class="px-6 py-4">{dog.Owner}</td>
        <td class="px-6 py-4">{dog.Age}</td>
        <td class="px-6 py-4">{dog.Breed}</td>
        <td class="px-6 py-4 flex gap-2 h-14">
          <svg
            class="cursor-pointer"
            on:click={() => handleEdit(dog)}
            on:keydown={() => handleEdit(dog)}
            data-modal-target="modal-edit"
            data-modal-toggle="modal-edit"
            fill="none"
            stroke="currentColor"
            stroke-width="1.5"
            viewBox="0 0 24 24"
            xmlns="http://www.w3.org/2000/svg"
            aria-hidden="true"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M16.862 4.487l1.687-1.688a1.875 1.875 0 112.652 2.652L6.832 19.82a4.5 4.5 0 01-1.897 1.13l-2.685.8.8-2.685a4.5 4.5 0 011.13-1.897L16.863 4.487zm0 0L19.5 7.125"
            />
          </svg>
          <svg
            class="cursor-pointer"
            on:click={() => handleDelete(dog.Id)}
            on:keydown={() => handleDelete(dog.Id)}
            fill="none"
            stroke="currentColor"
            stroke-width="1.5"
            viewBox="0 0 24 24"
            xmlns="http://www.w3.org/2000/svg"
            aria-hidden="true"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M14.74 9l-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 01-2.244 2.077H8.084a2.25 2.25 0 01-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 00-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 013.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 00-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 00-7.5 0"
            />
          </svg>
        </td>
      </tr>
    {/each}
  </tbody>
</table>

<Modal isEdit dogState={setDog} />
