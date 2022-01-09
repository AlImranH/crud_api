<template>
  <tr>
    <td style="width: 50px; align-item: center">{{post.id}}</td>
    <td>{{post.title}}</td>
    <td>{{post.body}}</td>
    <td style="width: 148px">
        <button class="mini ui blue button">Edit</button>
        <button class="mini ui red button" @click="onDelete">Delete</button>
    </td>
</tr>
</template>

<script>
export default {
    name: "Post",
    props:{
        post:{
            type: Object
        }
    },
    methods:{
        onDelete(){
            // console.log('Post delete ' + this.post.id);
            this.$emit('onDelete', this.post.id);
        }
    }
}
</script>

<style>

</style>