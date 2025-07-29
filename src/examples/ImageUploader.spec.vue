<script setup lang="ts">
import { shallowRef, useTemplateRef, ref } from "vue"
import { ImageUploader, type Image } from "@/components/ImageUploader"
import { message } from "@/scripts/client/message"

const imgs = shallowRef<Image[]>([])
const ImageUploaderRef = useTemplateRef("ImageUploaderRef")

const change = async (item: {
    images: Image[]
    action: "append" | "remove"
}) => {
    console.log(item)
    console.log(ImageUploaderRef.value?.size)
}

void (async function init() {
    const res = await fetch(`${import.meta.env.BASE_URL}data/Kirby.json`)
    const Kirby = (await res.json()) as Image
    if (Kirby.url)
        Kirby.url = Kirby.url.replace(/^\//, import.meta.env.BASE_URL)
    imgs.value = [Kirby]
})()

// 測試 `v-if`
const hidden = ref(false)
</script>
<template>
    <main style="display: contents">
        <ImageUploader
            v-if="!hidden"
            v-model="imgs"
            :limit="9"
            :accept="[`image/gif`, `image/jpeg`, `image/png`]"
            ref="ImageUploaderRef"
            @change="change"
            @over-limit="
                message({ content: `超出数量限制`, primary: `danger` })
            "
        />
        <p class="na-font-mono">
            {{ imgs.map((x: Image) => x.name) }}
        </p>
        <form onsubmit="return false">
            <div class="na-form-item">
                <span>hidden</span>
                <div class="na-input-wrapper">
                    <span class="na-switch sm">
                        <input
                            type="checkbox"
                            class="na-input"
                            v-model="hidden"
                            id="hidden"
                            name="hidden"
                        />
                        <i class="na-switch-mover"></i>
                        <label class="na-switch-slot" for="hidden"></label>
                    </span>
                </div>
            </div>
        </form>
    </main>
</template>
<style scoped>
button {
    margin-bottom: 16px;
}
</style>
