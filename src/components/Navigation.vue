<script setup>
import { RouterLink } from 'vue-router';
</script>

<template>
    <div class="navigation">
        <div class="navigation-wrapper">
            <div class="logo">
                <img src="@/assets/Vue_Logo_Black.png" />
                <h3 class="title">Vue Todo</h3>
            </div>
            <div class="menu">
                <ul class="nav-route">
                    <RouterLink :to="{name: 'todos'}">Home</RouterLink>
                    <RouterLink :to="{name: 'about'}">About</RouterLink>
                </ul>
            </div>
        </div>
    </div>
</template>

<style lang="scss">
.navigation {
    width: 100%;
    height: 80px;
    position: relative;
    background-color: rgba(207, 201, 201, 0.959);
    padding: 20px 10px;
}

.navigation-wrapper {
    display: flex;
    justify-content: space-between;   
    .logo {
        display: flex;
        align-items: center;
        flex-basis:80%;
        img {
            max-height: 50px;
            max-width: 50px;
        }
        .title{
            font-size: 32px;
        }
    }
    .menu{
        display: flex;
        align-items: center;
        flex-basis: 20%;
        .nav-route a{
            padding: 0 34px;
            font-size: 24px;
            text-decoration: none;
            color: inherit
        }
    }
}
</style>