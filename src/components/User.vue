<template>
    <div>
        <table class="style table">
            <tr class="style">
                <th class="style">ID</th>
                <th class="style">Title</th>
                <th class="style">Author</th>
            </tr>
            <tr class="style" v-for="(u, index) in load" :key="index">
                <td class="style">{{ u.id }}</td>
                <td class="style">{{ u.title }}</td>
                <td class="style">{{ u.author }}</td>
            </tr>
        </table>
        
    </div>
</template>
<script>
export default{
    props: ['load']

}
</script>
<style>
    .style {
        border: 1px solid black;
        border-collapse: collapse;
    }
    .table {
        margin: auto;
    }
</style>