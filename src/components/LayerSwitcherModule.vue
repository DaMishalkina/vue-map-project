<template>
    <div class="layers-menu__container">
        <h1>Layers</h1>
        <ul class="layers-menu__list">
            <li class="menu-item layers-menu__item">
                <label for="earthquake-layer">Earthquakes in California</label>
                <input type="checkbox" class="menu-item__checkbox" id="earthquake-layer" @click="$emit('choseLayer', $event)">
            </li>
            <li class="menu-item layers-menu__item">
                <label for="la-houses-layer">Houses built in Los Angeles since 2006</label>
                <input type="checkbox" class="menu-item__checkbox" id="la-houses-layer"
                       @click="$emit('choseLayer', $event)">

            </li>
            <li class="menu-item layers-menu__item">
                <label for="uk-residents-layer">UK residents work and residence places</label>
                <input type="checkbox" class="menu-item__checkbox"  id="uk-residents-layer" @click="$emit('choseLayer', $event)">
            </li>
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
        background-color: rgb(58, 69, 82);
        z-index: 1;
        width: 20%;
        height: 90%;
        border-radius: 2px;
        box-shadow: 0 2px 110px 0 rgba(0, 0, 0, 0.17);
    }
    h1 {
        margin: 0;
        padding: 0;
        margin-top: 20px;
        list-style: none;
        font-family: Helvetica, sans-serif;
        font-size: 20px;
        font-weight: lighter;
        color: #fff;
    }

    .layers-menu__list {
        margin: 0;
        display: flex;
        flex-wrap: wrap;
        padding: 10px;
    }
    .layers-menu__item {
        list-style: none;
        margin-top: 10px;
        height: 48px;
        padding: 10px 0px 0px 10px;
        font-family: Helvetica, sans-serif;
        color: rgb(160, 167, 180);
        background-color: rgb(41, 50, 60);
        border-radius: 12px;
        font-size: 12px;
        cursor: pointer;
    }
    .layers-menu__item:hover {
        opacity: 0.33;
    }
    .red{
        background-color: rgb(15, 150, 104);

    }
</style>