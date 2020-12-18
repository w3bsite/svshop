<script>
  import "node_modules/@glidejs/glide/dist/css/glide.theme.min.css";
  import "node_modules/@glidejs/glide/dist/css/glide.core.min.css";
  import "../public/css/mdb.min.css";
  import { onMount } from "svelte";
  import Glide from "@glidejs/glide";
  import { Icon } from "svelte-materialify/src";
  import Topbar from "./Topbar.svelte";
  import router from "page";
  import Gamess from "./Gamess.svelte";
  import { AppBar } from "svelte-materialify/src";
  import SingleGame from "./SingleGame.svelte";
  import Jumbo from "./jumbo.svelte";

  let theme = "dark";
  let page;
  let params;

  // ROUTER PAGE
  router("/", () => (page = app));
  router("/games", () => (page = Gamess));
  router(
    "/games/:id",
    (ctx, next) => {
      params = ctx.params;
      next();
    },
    () => (page = SingleGame)
  );
  router.start();
</script>

<style>
  .wrapper {
    min-height: 10000px;
  }
</style>

<div class="wrapper">
  <Topbar />

  <svelte:component this={page} {params} />
  <button type="button" class="btn btn-primary">Button
    <Icon disabled class="mdi mdi-account" /></button>
  <div class="col-md-6" />
</div>
