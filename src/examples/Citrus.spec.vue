<script setup lang="ts">
import { computed, ref } from "vue"
import { Citrus, type Item } from "@/components/Citrus"
import { message } from "@/scripts/client/message"

const count = ref(0)
const items = computed(() =>
    [
        { color: "rgb(var(--red-4)", key: "red" },
        { color: "rgb(var(--orange-4)", key: "orange" },
        { color: "rgb(var(--gold-4)", key: "gold" },
        { color: "rgb(var(--yellow-4)", key: "yellow" },
        { color: "rgb(var(--lime-4)", key: "lime" },
        { color: "rgb(var(--green-4)", key: "green" },
        { color: "rgb(var(--cyan-4)", key: "cyan" },
        { color: "rgb(var(--blue-4)", key: "blue" },
        { color: "rgb(var(--purple-4)", key: "purple" },
        { color: "rgb(var(--pinkpurple-4)", key: "pinkpurple" },
        { color: "rgb(var(--magenta-4)", key: "magenta" },
    ].slice(0, count.value)
)

function handleItemClick(item: Item) {
    console.log(item)
    const color = item.key as string
    message({
        content: color,
        primary: "primary",
        style: {
            "--background-color-message": `var(--${color}-5)`,
            "--box-shadow-color": `var(--${color}-4)`,
        },
    })
}
</script>
<template>
    <main style="display: contents">
        <section>
            <Citrus :items />
        </section>
        <section>
            <Citrus :items :stroke-width="18" @item-click="handleItemClick" />
        </section>
        <form onsubmit="return false">
            <div class="na-form-item">
                <label for="count">count</label>
                <div class="na-input-wrapper" data-validate>
                    <input
                        type="number"
                        class="na-input"
                        v-model="count"
                        id="count"
                        name="count"
                        :max="11"
                        :min="0"
                        required
                    />
                </div>
            </div>
        </form>
    </main>
</template>
<style scoped>
button {
    margin-bottom: 16px;
}
section {
    width: 120px;
}
</style>
