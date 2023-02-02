<script lang="ts">
  import Table from './Table.svelte'
  import Modal from './Modal.svelte'
</script>

<section class="h-[100vh] w-[50vw] p-10 ">
  <h2 class="text-4xl text-center mb-10">Dogs Database</h2>
  <!-- Modal toggle -->
  <button
    id="open-modal"
    data-modal-target="modal-create"
    data-modal-toggle="modal-create"
    class="block mb-4 text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
    type="button"
  >
    Add dog
  </button>
  <Modal />
  <Table />
</section>
