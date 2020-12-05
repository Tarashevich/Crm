<template>
    <ul class="sidenav app-sidenav" :class="{open: value}">

        <router-link
                v-for="link in links"
                :key="link.url"
                tag="li"
                :to="link.url"
                :exact="link.exact"
                active-class="active"
        >
            <a class="waves-effect waves-orange pointer">{{link.title}}</a>
        </router-link>
    </ul>
</template>

<script>
    export default {
        props: ['value'],
        data: () => ({
            links: [
                {url:'/', title:'Счет', exact: true},
                {url:'/history', title:'История'},
                {url:'/planning', title:'Планирование'},
                {url:'/record', title:'Новая запись'},
                {url:'/categories', title:'Категории'}
            ]
        })
    }
</script>