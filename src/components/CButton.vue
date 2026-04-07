<script setup>
import { createApp } from 'vue'


createApp(App).mount('#app');

var openButton = document.getElementById('product-card');
var closeButton = document.getElementById('close-drawer-button');
var drawer = document.querySelector('drawer');
var toggleDrawer = function (iWantItOpen) {
    if (iWantItOpen) {
        drawer.setAttribute('aria-hidden', 'false');
    }
    else {
        drawer.setAttribute('aria-hidden', 'true');
    }
};
document.addEventListener('DOMContentLoaded', function () {
    openButton.addEventListener('click', function () {
        toggleDrawer(true);
    });
    closeButton.addEventListener('click', function () {
        toggleDrawer(false);
    });
});
</script>

<template>
    <button id="close-drawer-button" class="btn">
        <slot></slot>
    </button>
</template>