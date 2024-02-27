<template>
    <div @click.self="closeModal">
        <div>
            <slot> fallback content...</slot>
            <div class="actions">
                <slot name="links"></slot>
            </div>
        </div>

    </div>
  
</template>

<script lang="js">
export default {
    emits: ['close'],
    methods: {
        closeModal() {
            this.$emit("close")
        }
    }

}
</script>

<style>

</style>