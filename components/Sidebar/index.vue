<template>
  <div>
    <div
      class="z-50 flex lg:hidden items-center justify-between w-full h-full p-4"
    >
      <Logo />
      <Icon
        class="absolute z-50 cursor-pointer right-4 top-4"
        size="30"
        name="iconamoon:menu-burger-horizontal"
        @click="open = true"
      />
      <div v-if="open" class="fixed top-0 left-0 z-50 w-full  h-full bg-white">
        <Icon
        class="absolute z-50 cursor-pointer right-4 top-4"
        size="30"
        name="material-symbols:close"
        @click="open = false"
      />
        <SidebarMenu/>
      </div>
    </div>
    <div
      class="hidden lg:flex w-[250px] h-screen flex flex-col justify-between border-r"
    >
      <SidebarMenu />
      <div>UserItem</div>
    </div>
  </div>
</template>

<script lang="ts" setup>
const open = ref(true);
</script>
