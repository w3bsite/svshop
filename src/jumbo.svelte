<script>
    import Icon from "svelte-materialify/src/components/Icon";
</script>

<div class="glide">
    <div class="glide__track" data-glide-el="track">
        <ul class="glide__slides">
            <slot>
                <!-- optional fallback -->
            </slot>
        </ul>
    </div>
    <div class="glide__arrows" data-glide-el="controls">
        <button class="glide__arrow glide__arrow--left  " data-glide-dir="<">
            <Icon class="mdi mdi-skip-previous orange-text" size="40px" />
        </button>
        <button
            class="glide__arrow glide__arrow--right mdi mdi-skip-next"
            data-glide-dir=">">
            <Icon class="mdi mdi-skip-next orange-text" size="40px" />
        </button>
    </div>
</div>
