<script lang="ts">
  export let id: string
  export let label: string
  export let value: string | number
</script>

<inputGroup>
  <label
    for={id}
    class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
  >
    {label}
  </label>
  <input
    {id}
    class="block w-full p-4 text-gray-900 border border-gray-300 rounded-lg bg-gray-50 sm:text-md focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
    bind:value
  />
</inputGroup>
