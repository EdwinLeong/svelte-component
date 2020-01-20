<script>
  export let title;

  let inlineCollapsed = false;

  export let items = [];

  let className = "";
  export { className as class };
  export let siderCollapsed = false;

  function toggle() {
    inlineCollapsed = !inlineCollapsed;
  }
</script>

<style>
  .folder {
    /* background-color: #777; */
    color: black;
    cursor: pointer;
    padding: 18px;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: baseline;
    /* width: 100%; */
    border: none;
    text-align: left;
    outline: none;
    font-size: 15px;
  }

  ul {
    list-style-type: none;
    line-height: 300%;
    padding: 0;
    margin: 0;
    list-style: none;
    background-color: #f1f1f1;
  }

  .file {
    text-align: left;
    padding: 18px;
    font-size: 15px;
  }

  .down {
    transform: rotate(45deg);
    -webkit-transform: rotate(45deg);
  }

  .up {
    transform: rotate(-135deg);
    -webkit-transform: rotate(-135deg);
  }

  i {
    border: solid rgb(29, 29, 29);
    border-width: 0 3px 3px 0;

    padding: 3px;

    float: right;
  }

  li {
    margin-left: 40px;
  }

  .siderCollapsed {
    width: 100%;
    border: 1px solid green;
    display: inline-block;
    line-height: 20px;
  }

  .siderCollapsed-content {
    display: none;
    /* float: right; */
    position: relative;
    background-color: #bbbbbb;
    /* min-width: 300px; */
    box-shadow: 0px 8px 16px 0px rgba(0, 0, 0, 0.2);
    z-index: 1;
    width: 300px;
  }

  .siderCollapsed-content ul {
    color: black;
    padding: 12px 16px;
    text-decoration: none;
    display: block;
    position: absolute;
    height: 300px;
    top: -50px;
    left: 100%;
    width: 100%;
  }

  .siderCollapsed-content ul:hover {
    background-color: #ddd;
    width: 300px;
  }

  .siderCollapsed:hover .siderCollapsed-content {
    display: block;
  }
</style>

{#if siderCollapsed}
  <div class:siderCollapsed>
    <div class="folder">
      <span>{title}</span>
    </div>
    <div class="siderCollapsed-content">
      <ul>
        {#each items as { id, title, submenu }}
          <li class={submenu ? '' : 'file'}>
            {#if submenu}
              <svelte:self items={submenu} {title} />
            {:else}{title}{/if}
          </li>
        {/each}
      </ul>

      <!-- {#each items as { id, title, submenu }}
        {#if submenu}
          <ul>
            <li>
              <svelte:self items={submenu} {title} />
            </li>
          </ul>
        {:else}
          <ul>
            <li class="file">{title}</li>
          </ul>
        {/if}
      {/each} -->

    </div>
  </div>
{:else}
  <div class="folder" on:click={toggle}>
    <span class:inlineCollapsed>{title}</span>
    {#if inlineCollapsed}
      <i class="up" />
    {:else}
      <i class="down" />
    {/if}
  </div>
  {#if inlineCollapsed}
    <ul>
      {#each items as { id, title, submenu }}
        {#if submenu}
          <li>
            <svelte:self items={submenu} {title} />
          </li>
        {:else}
          <li class="file">{title}</li>
        {/if}
      {/each}
    </ul>
  {/if}
{/if}

<!-- <li style="border: 1px solid green;background:blue"></li> -->
<!-- markup (zero or more items) goes here -->
<!-- {#if submenu}
        <ul>
          <li style="margin-left:40px">
            <svelte:self items={submenu} {title} />

          </li>
        </ul>
      {:else}
        <li class="file">{title}</li>
      {/if} -->
