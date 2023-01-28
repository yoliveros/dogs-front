<script lang="ts">
  import Table from './Table.svelte'
  import Modal from './Modal.svelte'
  import Form from './Form.svelte'
</script>

<section class="h-[100vh] w-[50vw] p-10 ">
  <h2 class="text-4xl text-center mb-10">Dogs Database</h2>
  <Modal>
    <Form />
  </Modal>
  <Table />
</section>
