<script>
  import Thir from "./Thir.svelte";
  import Fir from "./Fir.svelte";
  import Gamess from "./Gamess.svelte";

  import {
    Tabs,
    Tab,
    Window,
    WindowItem,
    AppBar,
    Card,
    Button,
  } from "svelte-materialify/src";
  import Jumbo from "./jumbo.svelte";

  let value = [0];

  export let duration = "300ms";
  export let offset = 0;
  export let tolerance = 0;

  let headerClass = "show";
  let y = 0;
  let lastY = 0;
  let flat = false;
  let el;

  function deriveClass(y, dy) {
    if (y < offset) {
      return "show";
    }

    if (Math.abs(dy) <= tolerance) {
      return headerClass;
    }

    if (dy > 0) {
      return "show";
    }

    return "hide";
  }

  function updateClass(y) {
    const dy = lastY - y;
    lastY = y;
    return deriveClass(y, dy);
  }

  function setTransitionDuration(node) {
    node.style.transitionDuration = duration;
  }

  $: headerClass = updateClass(y);
  $: ele(y);
  function ele(y) {
    if (y <= 25) {
      return (el = 1);
    } else {
      el = 3;
    }
  }
</script>

<style>
  .tabContent {
    /* margin-top: 140px; */
  }
  .nav {
    width: 100%;
    top: 0px;

    z-index: 99;
    transition: 300ms linear;
    position: fixed !important;
  }
  .bar {
    width: 100%;
    top: 20px;
    z-index: 55;
    transition: transform 300ms linear;
    position: fixed !important;
  }

  .show {
    transform: translateY(0%);
  }

  .hide {
    transform: translateY(-400%);
  }

  .tabContent {
    margin-top: 300px;
  }
  .nwrap {
    /* background-color: violet !important;
    position: initial;
    padding-top: 1%; */
  }
</style>

<svelte:window bind:scrollY={y} />
<div class="  nwrap">
  <!-- TopNAV -->
  <div class=" nav white card ">
    <Card class=" elevation-{el}   d-flex flex-row" {flat}>
      <span style=" flex-grow:18 " />

      <div style=" flex-grow:1">
        <img src="icons8-skyrim.svg " alt="logo" />Fit-Shop
      </div>
    </Card>
  </div>
  <!-- BottomNAV -->
  <div use:setTransitionDuration class="{headerClass} white bar   ">
    <AppBar class="elevation-{el}  " {flat}>
      <span slot="title"> Title </span>
      <div slot="extension">
        <Tabs class="green-text" bind:value fixedTabs>
          <div slot="tabs">
            <Tab>Item 1</Tab>
            <Tab>Item 2</Tab>
            <Tab>Item 3</Tab>
          </div>
        </Tabs>
      </div>
    </AppBar>
  </div>
</div>

<div class="tabContent">
  <Card>
    <Window value={value[0]} class="ma-4 ">
      <WindowItem>
        Item 1
        <Gamess />
      </WindowItem>
      <WindowItem>
        <h4>Item 2</h4>
        <Fir />
      </WindowItem>
      <WindowItem>
        <h4>Item 3</h4>
        <p>
          <Thir />
        </p>
      </WindowItem>
      <WindowItem>
        <h4>Item</h4>

        <slot />
      </WindowItem>
    </Window>
  </Card>
</div>
