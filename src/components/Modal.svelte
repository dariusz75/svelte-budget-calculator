<script>
  import { fade, fly } from 'svelte/transition';
</script>

<div class="modal-container" transition:fade>
  <div class="modal-content" transition:fly={{ y: 200 }}>
    <slot>default text</slot>
  </div>
</div>
