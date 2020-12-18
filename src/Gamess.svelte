<script>
    import { onMount } from "svelte";
    import Card from "svelte-materialify/src/components/Card";

    let data = [];

    let url = "https://dlfox.com/wp-json/wp/v2/posts";
    let proxy = "http://localhost:8080/";

    onMount(async function gett() {
        const res = await fetch(proxy + url);
        data = await res.json();
    });
</script>

<div class="container">
    <h1>Gaa</h1>
    <div class="row">
        {#each data as item}
            <div class="col">
                <Card>
                    {@html item.content.rendered}
                </Card>
            </div>
        {/each}
    </div>
</div>
