<script>
  export let href;
  export let blank = true
  let show_link = false;
  export let setLink;
  function toggleLink(e) {
    show_link = !show_link;
    stop(e);
  }
  function stop(e) {
    e.preventDefault();
    e.stopPropagation();
    return false;
  }
  function hideLink() {
    show_link = false;
  }

  function addLink() {
    setLink(`link`, href, {blank});
    hideLink();
  }

  function rmLink() {
    setLink("link", null);
    hideLink();
  }
  
  if(window)
        window.__edw.addEventListener('click', hideLink)
</script>

<div class="relative" on:mousedown>
  <span class="px-2 py-1" on:click={toggleLink}>
    <span class="border-b border-gray-400">Link</span>
  </span>
  {#if show_link}
    <div
      class="absolute p-3 shadow-xl flex rounded bg-white -ml-24 mt-1 z-920 z-20"
      on:click={stop}>
      <input
        on:click={stop}
        on:focus={stop}
        type="text"
        bind:value={href}
        placeholder="Past your link, such as http://fouita.com"
        class="bg-gray-100 border p-1 w-64 rounded outline-none
        shadow-inner" />
      <button
        class="ml-2 hover:bg-gray-300 px-3 rounded outline-none"
        on:click={addLink}>
        Link
      </button>
      <button
        class="hover:bg-gray-300 px-3 rounded outline-none"
        on:click={rmLink}>
        Unlink
      </button>
      <label class="flex items-center text-black text-xs" on:click|stopPropagation>
        <input type="checkbox" bind:checked={blank} class="mr-2" />
        NewTab
      </label>
    </div>
  {/if}
</div>
