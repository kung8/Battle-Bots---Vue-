<template>
    <div>   
        <p>Name:{{bot.name}}</p>
        <p>Attack:{{bot.attack}}</p>
        <p>Health:{{bot.health}}</p>
        <button @click='select(bot)'>Select</button>
        <button @click='retire(index)'>Retire</button>
        <hr>
    </div>
</template>

<script>
export default {
    props:['bot','index','retire','select']
}
</script>

<style>

</style>
