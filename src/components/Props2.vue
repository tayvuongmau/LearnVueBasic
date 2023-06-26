<template>
    <div>
        <div id="font">{{ PropsSecond.name }}</div>
    </div>
</template>
<script>
export default{
    props: ['PropsSecond']
}
</script>
<style scoped>
    #font{
        font-weight: lighter;
        color: red;
        border: 1px solid black;
        background-color: cadetblue;
    }
</style>