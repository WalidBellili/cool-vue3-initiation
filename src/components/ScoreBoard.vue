<template>
    <section>
        Player <span>{{this.winCount}}</span> x <span>{{this.looseCount}}</span> computer
    </section>
</template>

<script>
export default {
    props : {
        winCount: Number,
        looseCount: Number,
    }

}

</script>

<style>

</style>