<script lang="ts">
  export let id: string
  export let label: string
  export let value: string | number
  export let required: boolean
</script>

<inputGroup>
  <label for={id} class="block mb-2 text-sm font-medium text-white">
    {label}
  </label>
  <input
    {id}
    class="block w-full p-4 border rounded-lg sm:text-md bg-gray-800 border-gray-600 placeholder-gray-400 text-white focus:ring-blue-500 dark:focus:border-blue-500"
    bind:value
    {required}
  />
</inputGroup>
