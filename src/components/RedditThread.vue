<template>
  <!-- TOOLTIP -->
  <button :onClick="thread.url" class="thread"
          :title="`Title: ${thread.title}
                   Author: ${thread.author}
                   Comments: ${thread.num_comments}
                   Score: ${thread.score}`">
    <h3>{{thread.title}}</h3>
    <label>{{ thread.author }}</label>
    <div id="col2">
      <label >Preview:</label>
      <object type="text/html" :data="thread.url" width="500px">
      </object>
    </div>
  </button>
</template>

<script>
export default {
  name: "reddit-thread",
  props: ['thread']
}
</script>
<style>

</style>