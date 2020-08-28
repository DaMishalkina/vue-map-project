<template>
    <div class="layers-menu__container">
        <h1>Layers</h1>
        <ul class="layers-menu__list">
            <li class="layers-menu__item" id="earthquake-layer" @click="$emit('choseLayer', $event)">Earthquakes in California</li>
            <li class="layers-menu__item" id="la-houses-layer" @click="$emit('choseLayer', $event)">Houses built in Los Angeles since 2006.</li>
            <li class="layers-menu__item" id="uk-residents-layer" @click="$emit('choseLayer', $event)">UK residents work and residence places</li>
        </ul>
    </div>
</template>

<script>
    export default {
        name: "UK_citizens_layer"
    }
</script>

<style scoped>
    .layers-menu__container{
        position: absolute;
        top: 10px;
        left: 10px;
        padding: 10px;
        background-color: rgb(169, 169, 169);
        z-index: 1;
        width: 20%;
        height: 90%;
        border-radius: 6px;
        box-shadow: 0 2px 110px 0 rgba(0, 0, 0, 0.17);
    }
    h1 {
        margin: 0;
        padding: 0;
        list-style: none;
        font-family: Roboto, sans-serif;
        color: #000;
        text-shadow: 0px 1px 6px #fff;
        text-align: center;
    }

    .layers-menu__list {
        display: flex;
        flex-wrap: wrap;
        padding: 10px;
    }
    .layers-menu__item {
        list-style: none;
        margin-top: 10px;
        font-family: Roboto, sans-serif;
        color: #fff;
        font-size: 16px;
        cursor: pointer;
    }
    .layers-menu__item:hover, .layers-menu__item:focus {
        background-color: rgb(196, 97, 140);
    }
</style>