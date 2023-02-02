<script lang="ts">
  import Form from './Form.svelte'
  import type Dog from './Dog'

  export let dogState: Dog = {
    Id: '',
    Name: '',
    Owner: '',
    Breed: '',
    Age: 0
  }

  export let isEdit = false
</script>

<!-- Main modal -->
<div
  id={isEdit ? 'modal-edit' : 'modal-create'}
  tabindex="-1"
  aria-hidden="true"
  class="fixed top-0 left-0 right-0 z-50 hidden w-full p-4 overflow-x-hidden overflow-y-auto md:inset-0 h-modal md:h-full"
>
  <div class="relative w-full h-full max-w-md md:h-auto">
    <!-- Modal content -->
    <div class="relative rounded-lg shadow bg-gray-700">
      <button
        id="close-modal"
        type="button"
        class="absolute top-3 right-2.5 rounded-lg text-sm p-1.5 ml-auto inline-flex items-center hover:bg-gray-800 hover:text-white"
        data-modal-hide={isEdit ? 'modal-edit' : 'modal-create'}
      >
        <svg
          aria-hidden="true"
          class="w-5 h-5"
          fill="currentColor"
          viewBox="0 0 20 20"
          xmlns="http://www.w3.org/2000/svg"
          ><path
            fill-rule="evenodd"
            d="M4.293 4.293a1 1 0 011.414 0L10 8.586l4.293-4.293a1 1 0 111.414 1.414L11.414 10l4.293 4.293a1 1 0 01-1.414 1.414L10 11.414l-4.293 4.293a1 1 0 01-1.414-1.414L8.586 10 4.293 5.707a1 1 0 010-1.414z"
            clip-rule="evenodd"
          /></svg
        >
        <span class="sr-only">Close modal</span>
      </button>
      <div class="px-6 py-6 lg:px-8">
        <h3 class="mb-4 text-xl font-medium text-white">
          {isEdit ? 'Edit dog' : 'Add new dog'}
        </h3>
        <!-- <slot {isEdit} /> -->
        <Form {isEdit} {dogState} />
      </div>
    </div>
  </div>
</div>
