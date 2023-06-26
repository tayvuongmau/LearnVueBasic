<template>
    <div>
        <div id="font">{{ clubProps.name }} - {{ clubProps.country }}</div>
    </div>
</template>

<script>
export default{
    props:['clubProps']
}
</script>

<style scoped>
    #font {
        font-weight: bold;
        color: green;
        border: 2px solid red;
        padding: 1px;
        margin: 3px;
        background-color: aquamarine;
    }
</style>