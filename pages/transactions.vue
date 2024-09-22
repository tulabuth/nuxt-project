<script setup>
import { Button } from '~/components/ui/button';

    const loading = ref(false)
</script>

<template>
   <div>
    <header>
        <h1>Dashboard</h1>
    </header>
    <main>
        <div>
        Tabs: Today This week This month This year
        </div>
        <section>
            Chart
        </section>
    </main>
    <footer>
        This is my footer
    </footer>
   </div>
</template>