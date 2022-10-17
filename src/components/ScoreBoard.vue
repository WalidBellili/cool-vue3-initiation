<template>
    <section>
        Player <span>{{this.winCount}}</span> x <span>{{this.looseCount}}</span> computer
    </section>
</template>

<script>
export default {
    props : ["winCount", "looseCount"]

}

</script>

<style>

</style>