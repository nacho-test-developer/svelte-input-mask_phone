<script>
  import { onMount } from "svelte";

  let data = [];
  let cities = [];
  let searchValue = null;
  let db =
    "https://gist.githubusercontent.com/nacho-test-developer/11cbcf693e83f37921b842e3f785e701/raw/38acee6b78ff2fbd3929891669e6b7cd775e4f77/code.json";

  // Fetch DB
  onMount(async function() {
    const response = await fetch(`${db}`);
    try {
      const json = await response.json();
      data = json;
    } catch (e) {}
  });

  // Keydown event
  function handleKeydown(event) {
    if (event.key === "Enter") {
      return search(searchValue);
    }
  }

  // Search Method
  function search(val) {
    // search by code
    const result = data.filter(item => item.code === 11);
    // list of cities from code search
    let found = result[0].city;
    if (found) {
      // new cities array
      cities = found.split(",");
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
          bind:value={searchValue}
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