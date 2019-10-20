<script>
  import { onMount } from "svelte";

  let data = [];
  let otros = [];
  let cities = [];
  let search = null;
  let result = null;
  let filtered = null;
  let db =
    "https://gist.githubusercontent.com/nacho-test-developer/11cbcf693e83f37921b842e3f785e701/raw/38acee6b78ff2fbd3929891669e6b7cd775e4f77/code.json";

  onMount(async function() {
    const response = await fetch(`${db}`);
    try {
      const json = await response.json();
      data = json;
    } catch (e) {}
  });

  function handleKeydown(event) {
    if (event.key === "Enter") {
      return buscar(search);
    }
  }

  function buscar(val) {
    let result = data.filter(aa => aa.code === 11);
    let result2 = result[0].city;
    if (result2) {
      cities = result2.split(",");
      return cities;
    }
  }
</script>

<main>
  <div class="w-full">
    <div class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
      <div class="mb-4">
        <label
          class="block text-gray-700 text-sm font-bold mb-2"
          for="search"
        >
          Buscar por código de área
        </label>
        <input
          class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
          id="search"
          placeholder="Ej: 351"
          type="text"
          bind:value={search}
          on:keydown={handleKeydown}
        >
      </div>
    </div>
  </div>
  <p class="m-6">
    Se encontraron 
    {#if cities}
    <strong>{cities.length}</strong>
    {/if}localidades.
  </p>

  {#each cities as city}
    <hr />
    <div class="px-6 py-4">{city}</div>
    <hr />
  {/each}

</main>