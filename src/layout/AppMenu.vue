<script setup>
import { ref } from 'vue';

import AppMenuItem from './AppMenuItem.vue';

const model = ref([
    {
        label: 'Gestión',
        items: [{ label: 'Personas', icon: 'pi pi-fw pi-home', to: '/' }]
    },
    {
        label: 'Documentos',
        items: [
            { label: 'Documentos', icon: 'pi pi-fw pi-id-card', to: '/documentos' },
            { label: 'Asignació de Documentos', icon: 'pi pi-fw pi-check-square', to: '/uikit/input' }
            
        ]
    }
]);
</script>

<template>
    <ul class="layout-menu">
        <template v-for="(item, i) in model" :key="item">
            <app-menu-item v-if="!item.separator" :item="item" :index="i"></app-menu-item>
            <li v-if="item.separator" class="menu-separator"></li>
        </template>
    </ul>
</template>

<style lang="scss" scoped></style>
