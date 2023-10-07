<script setup lang="ts">
import CronGenerator from "./cronGenerator/index.vue";
import { ref } from "vue";

const cronExpression = ref("* * * * * * *");
const handleExpChange = (exp: string) => {
    cronExpression.value = exp;
};
const cronRef = ref<typeof CronGenerator>();
const getResult = () => {
    console.log(cronRef.value?.getResultTime());
};
</script>

<template>
    <CronGenerator
        ref="cronRef"
        :cron-expression="cronExpression"
        @exp-change="handleExpChange"
    ></CronGenerator>
    <a-input v-model:value="cronExpression"></a-input>
    <a-button @click="getResult">获取运行时</a-button>
</template>

<style scoped></style>
