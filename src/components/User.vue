<template>
    <div>
        <table>
            <tr>
                <th>ID</th>
                <th>Title</th>
                <th>Author</th>
            </tr>
            <tr>
                <td>{{ load.id }}</td>
                <td>{{ load.title }}</td>
                <td>{{ load.author }}</td>
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

</style>