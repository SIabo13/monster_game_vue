<template>
    <div>
        <h1 class="text-center">Monster</h1>
        <div class="progress">
  <div class="progress-bar progress-bar-striped bg-success" role="progressbar" :style="{width: health + '%'}" aria-valuenow="25" aria-valuemin="0" aria-valuemax="100"></div>
</div>
    </div>
</template>
<script>
export default {
    props:['health']
    
}
</script>

<style scoped>

</style>