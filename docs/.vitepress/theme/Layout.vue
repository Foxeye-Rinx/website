<script setup lang="ts">
import 'vuetify/styles';
import DefaultTheme from 'vitepress/theme';
import Footer from './components/Footer.vue';
import Sponsors from './components/Sponsors.vue';
import SidebarBefore from './components/SidebarBefore.vue';
import { watchEffect } from 'vue';
import { useData } from 'vitepress';
import { useTheme } from 'vuetify';
import './styles/main.scss';
import HomeImage from './components/HomeImage.vue';

const { Layout } = DefaultTheme;

const { isDark } = useData();
const theme = useTheme();

watchEffect(() => {
  theme.global.name.value = isDark.value ? 'dark' : 'light';
});
</script>

<template>
  <div :class="isDark ? 'v-theme--dark' : 'v-theme--light'">
    <Layout>
      <template #sidebar-nav-before>
        <SidebarBefore />
      </template>
      <template #layout-bottom>
        <Footer />
      </template>
      <template #aside-ads-before>
        <Sponsors />
      </template>
      <template #home-hero-image>
        <ClientOnly>
          <HomeImage />
        </ClientOnly>
      </template>
    </Layout>
  </div>
</template>
