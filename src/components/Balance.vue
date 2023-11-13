<template>
    <h4>Your Balance</h4>
    <h1 id="balance">P {{ total }}</h1>
</template>

<script>
export default {
    props: ["total"],
};
</script>
