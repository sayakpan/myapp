<template>
    <header class="d-flex justify-content-center py-3">
        <ul class="nav nav-pills">
            <li class="nav-item"><Nuxt-link to="/" class="nav-link active" aria-current="page">Home</Nuxt-link></li>
            <li class="nav-item"><Nuxt-link to="/explore" class="nav-link">Explore</Nuxt-link></li>
            <li class="nav-item"><Nuxt-link to="/features" class="nav-link">Features</Nuxt-link></li>
            <li class="nav-item"><Nuxt-link to="/faq" class="nav-link">FAQs</Nuxt-link></li>
            <li class="nav-item"><Nuxt-link to="/about" class="nav-link">About</Nuxt-link></li>
        </ul>
    </header>
</template>

<script>
export default {
  name: "NavBar",
}
</script>