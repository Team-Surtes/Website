<template>
  <div id="navigation" :data-drawer-state="drawerIsOpen" class="z-50 sticky top-0">
      <header :style="{ backgroundColor: headerBackgroundColor }" class="glass fixed top-0 left-0 right-0 h-24 px-8 py-4 bg-surtes-950 flex justify-between text-center">
          <div id="logo" class="h-full" :class="{ 'mx-auto': !drawerIsOpen, 'transition-all duration-500': true, 'h-16': drawerIsOpen }">
              <NuxtLink to="/">
                  <NuxtImg src="/surtes-logo.svg" class="h-full mx-auto" />
              </NuxtLink>
          </div>
          <nav id="drawer-links" class="flex mt-4" v-if="drawerIsOpen">
            <div class="flex gap-x-12 font-black text-white overflow-x-auto no-scrollbar">
              <NuxtLink to="/blog" class="h-12 transform hover:scale-110" @click="drawerIsOpen = false">News Articles</NuxtLink>
              <NuxtLink to="/sponsors" class="h-12 transform hover:scale-110" @click="drawerIsOpen = false">Our Sponsors</NuxtLink>
              <NuxtLink to="/electric" class="h-12 transform hover:scale-110" @click="drawerIsOpen = false">SURTES Electric</NuxtLink>
              <NuxtLink to="/combustion" class="h-12 transform hover:scale-110" @click="drawerIsOpen = false">SURTES Combustion</NuxtLink>
            </div>
          </nav>
          <button id="b1" class="block h-full w-16 transform hover:scale-110 rounded-md p-0" @click="drawerIsOpen = !drawerIsOpen">
            <Icon  :name="drawerIsOpen ? 'ic:round-close' : 'ic:baseline-dehaze'" color="white" class="text-3xl lg:text-2xl" />
          </button>
      </header>
  </div>
</template>

<style scoped lang="scss">
#navigation > header {
  background: var(--header-bg);
}

#logo{
  // height: 4.75rem;
  transition: height 0.5s;
  align-items: center;
}

.glass {
  background: rgba( 69, 12, 10, 0.75 );
  box-shadow: 0 8px 32px 0 rgba( 69, 12, 10, 0.37 );
  backdrop-filter: blur( 5px );
  -webkit-backdrop-filter: blur( 5px );
}

.no-scrollbar {
  scrollbar-width: none;
  -ms-overflow-style: none;
  padding-right: 1rem;
  &::-webkit-scrollbar {
    display: none;
  }
}

@media screen and (max-width: 768px) {
  #drawer-links {
    overflow-x: auto;
    overflow-y: hidden;
  }
}
</style>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue';

let drawerIsOpen = ref(false);
let headerBackgroundColor = ref('rgba( 69, 12, 10, 0.75 )');
const handleScroll = () => {
  // Calculate scroll pct
  const scrollPercentage = (window.scrollY / window.innerHeight) * 100;

  // Determine what color to show
  if (scrollPercentage >= 75) {
    headerBackgroundColor.value = '#450c0a';
  } else{
    headerBackgroundColor.value = 'rgba( 69, 12, 10, 0.75 )';
  }
};

onMounted(() => {
  window.addEventListener('scroll', handleScroll);
});

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll);
});
</script>
