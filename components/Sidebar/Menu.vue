<template>
  <div>
    <header class="flex items-center gap-2 p-4 hover:scale-[101%] transition cursor-pointer">
        <Logo/>
        <div class="font-bold">Nuxt-Finance</div>
    </header>
    <div class="px-4 grow">
        <div class="grid gap-4">
            <NuxtLink :href="item.path" v-for='(item,index) in items' :key='index'
            class="flex items-center gap-2 px-2 py-1 transition rounded cursor-pointer hover:bg-neutral-100"
            >
            <Icon v-if="item.icon" size="20" :name="item.icon" style="color: black" />
                <span>{{ item.title }}</span>
            </NuxtLink>
        </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import Logo from '../Logo.vue';

    const items =ref([
        {
            title: "Overview",
            path: "/",
            icon: "ri:dashboard-line"
        },{
            title: "Transactions",
            path: "/transactions",
            icon:"ph:arrows-left-right"
        },{
            title: "Account",
            path: "/account",
            icon:"material-symbols:account-box-sharp"
        },{
            title: "Contacts",
            path: "/contacts",
            icon: "mingcute:contacts-3-fill"
        },{
            title: "Settings",
            path: "/settings",
            icon: "uil:setting"
        }
    ])
</script>