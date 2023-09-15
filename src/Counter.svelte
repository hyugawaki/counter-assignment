<script lang="ts">
  export let count: number;
  export let input: string;

  function increment() {
    count += 1;
  }

  function decrement() {
    if (count > 0) {
      count -= 1;
    }
  }

  function reset() {
    count = 0;
  }
</script>

<div
  class="flex inline-flex flex-col items-center justify-center border rounded p-4"
>
  <input
    type="text"
    placeholder="type title..."
    class="h-6 border border-gray-200 rounded placeholder-gray-300"
    bind:value={input}
  />
  <div>
    <p class="py-2">{count}</p>
    <button on:click={increment} class="bg-red-300 px-2 rounded">+</button>
    <button on:click={decrement} class="bg-sky-300 px-2 rounded">-</button>
    <button on:click={reset} class="border px-2 rounded">Reset</button>
  </div>
</div>
