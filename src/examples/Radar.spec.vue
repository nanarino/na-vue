<script setup lang="ts">
import { Radar, type Points } from "@/components/Radar"
import { line, curveCardinalClosed } from "d3-shape"

const smoothing = (points: Points) => {
    return line().curve(curveCardinalClosed.tension(0.3))(points) as string
}

const columnsData = {
    price: "Price",
    useful: "Usefulness",
    design: "Design",
    battery: "Battery Capacity",
    camera: "Camera Quality",
}

const data = [
    {
        class: "iphone",
        price: 1,
        battery: 0.7,
        design: 1,
        useful: 0.9,
        camera: 0.9,
    },
    {
        class: "galaxy",
        price: 0.8,
        battery: 1,
        design: 0.6,
        useful: 0.8,
        camera: 1,
    },
    {
        class: "nexus",
        price: 0.5,
        battery: 0.8,
        design: 0.7,
        useful: 0.6,
        camera: 0.6,
    },
]
</script>
<template>
    <view style="display: contents">
        <Radar
            class="my-phone"
            :columns-data
            :data
            :options="{
                scales: 5,
                smoothing,
                shapeProps(data) {
                    return {
                        title: data.class,
                        class: 'shape ' + data.class,
                    }
                },
            }"
        />
    </view>
</template>
<style scoped>
:deep(.my-phone) {
    .axis {
        stroke: rgb(var(--gray-6));
        stroke-width: 0.2;
    }

    .scale {
        stroke: rgb(var(--gray-4));
        stroke-width: 0.2;
    }

    .shape {
        fill-opacity: 0.3;
        stroke-width: 0.5;
    }

    .shape:hover {
        fill-opacity: 0.6;
    }

    .shape.iphone {
        fill: rgb(var(--cyan-4));
        stroke: rgb(var(--cyan-6));
    }

    .shape.nexus {
        fill: rgb(var(--yellow-4));
        stroke: rgb(var(--yellow-6));
    }

    .shape.galaxy {
        fill: rgb(var(--pinkpurple-4));
        stroke: rgb(var(--pinkpurple-6));
    }
}
</style>
