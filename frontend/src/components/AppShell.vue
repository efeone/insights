<template>
	<div class="mx-auto flex h-full w-full max-w-[1440px] text-base">
		<Sidebar v-if="!hideSidebar" />
		<div
			class="flex flex-1 flex-col pl-2"
			:class="[hideSidebar ? 'ml-4 w-[calc(100%-1rem)]' : 'ml-[15rem] w-[calc(100%-15rem)]']"
		>
			<RouterView :key="$route.fullPath" />
		</div>
	</div>
</template>

<script setup>
import { computed } from 'vue'
import auth from '@/utils/auth'
import settings from '@/utils/settings'
import { setupComplete } from '@/utils/setupWizard'
import Sidebar from '@/components/Sidebar.vue'
import { useRoute } from 'vue-router'

const route = useRoute()
const hideSidebar = computed(() => {
	return (
		route.meta.hideSidebar || !setupComplete.value || !auth.isLoggedIn || settings.hideSidebar
	)
})
</script>
