<template>
    <div class="result">
        <div class="title">{{ this.result.title }}</div>
        <div class="desc">{{ this.result.desc }}</div>
    </div>
</template>

<script>
export default {
    name: "result-component",
    props: ["result"],
};
</script>
