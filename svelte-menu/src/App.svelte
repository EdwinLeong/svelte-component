<script>
  import Folder from "./Folder.svelte";
  export let name;

  let siderCollapsed = true;
  function onClick() {
    siderCollapsed = !siderCollapsed;
  }
  export let count = 3;

  let menus = [
    {
      id: 1,
      level: 1,
      title: "Option 1",
      submenu: [
        {
          id: 1.0,
          title: "Option 1.0 Lvl2",
          submenu: [
            { id: "1.0.1", title: "Option 1.0.1 Lvl2" },
            { id: "1.0.2", title: "Option 1.0.2 Lvl2" },
            {
              id: "1.0.3",
              title: "Option 1.0.3 Lvl2",
              submenu: [
                { id: "1.0.1", title: "Option 1.0.1 Lvl2" },
                { id: "1.0.2", title: "Option 1.0.2 Lvl2" },
                { id: "1.0.3", title: "Option 1.0.3 Lvl2" }
              ]
            }
          ]
        },
        { id: 1.1, title: "Option 1.1 Lvl2" },
        { id: 1.2, title: "Option 1.2 Lvl2" }
      ]
    },
    {
      id: 2,
      title: "Option 2",
      submenu: [
        { id: 2.0, title: "Option 2.0 Lvl2" },
        { id: 2.1, title: "Option 2.1 Lvl2" },
        { id: 2.2, title: "Option 2.2 Lvl2" }
      ]
    },
    {
      id: 3,
      title: "Option 3",
      submenu: [
        { id: 3.0, title: "Option 3.0 Lvl2" },
        { id: 3.1, title: "Option 3.1 Lvl2" },
        { id: 3.2, title: "Option 3.2 Lvl2" }
      ]
    },
    { title: "Navigation One", submenu: [] }
  ];
</script>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }

  .container {
    display: inline-block;
    cursor: pointer;
    background-color: #fff;
    width: 80px;
    height: 32px;
    border: 1px solid rgb(184, 183, 183);
    border-radius: 5px;
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
    align-items: center;
  }

  .bar1,
  .bar2,
  .bar3 {
    width: 25px;
    height: 3px;
    background-color: #1890ff;
    transition: 0.4s;
  }

  li {
    list-style-type: none;
    line-height: 300%;
    padding: 0;
    margin: 0;
    width: 100%;
    list-style: none;
    background-color: #d8d8d8;
  }

  li:hover {
    background-color: rgb(116, 116, 116);
  }
</style>

<main>

  <h1>Hello {name}!</h1>
  <p>
    Visit the
    <a href="https://svelte.dev/tutorial">Svelte tutorial</a>
    to learn how to build Svelte apps.
  </p>
  <div class="container" on:click={onClick}>
    <div class="bar1" />
    <div class="bar2" />
    <div class="bar3" />
  </div>
  <ul style="width:{siderCollapsed ? '300px' : '500px'}">
    {#each menus as menu}
      <li>
        <Folder title={menu.title} items={menu.submenu} {siderCollapsed} />
      </li>
    {/each}
  </ul>
  <!-- {#each menus as { id, title, submenu }}
      <li>
        <Folder {title} items={submenu} />
      </li>
    {/each} -->

  <!-- <Folder title="" items={menus} {siderCollapsed} /> -->

</main>
