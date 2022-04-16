<template>
    <div class="wrapper-layaut">
        <NavBarSite />
        <main>
            <Nuxt />
        </main>
    </div>
</template>
<script>
import NavBarSite from '../components/NavBarSite.vue'
export default {
    components: { NavBarSite },

}
</script>
