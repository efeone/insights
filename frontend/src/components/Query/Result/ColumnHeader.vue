<template>
	<div v-if="props.column" class="group flex items-center justify-between">
		<div class="flex items-center">
			<!-- <span
				v-if="props.column.aggregation"
				class="my-0 mr-2 flex-1 select-none whitespace-nowrap rounded border border-orange-200 px-1 py-0.5 text-xs text-orange-400/80"
			>
				{{ props.column.aggregation }}
			</span> -->
			<div class="rounded text-base">{{ props.column.label }}</div>
		</div>
		<div class="flex select-none items-center justify-end">
			<!-- show sort options only if column is from doc.columns -->
			<div
				v-if="props.column.name"
				@click.prevent.stop="orderByColumn"
				class="ml-4 cursor-pointer py-1 text-gray-500 hover:text-gray-800"
			>
				<FeatherIcon
					v-if="props.column.order_by == 'asc'"
					name="arrow-up"
					class="mx-1 h-3 w-3"
				/>
				<FeatherIcon
					v-else-if="props.column.order_by == 'desc'"
					name="arrow-down"
					class="mx-1 h-3 w-3"
				/>
				<FeatherIcon v-else name="code" class="mx-1 h-3 w-3 rotate-90" />
			</div>
		</div>
	</div>
</template>

<script setup>
import { inject } from 'vue'

const query = inject('query')
const props = defineProps({
	column: {
		type: Object,
		required: true,
	},
})

const orderByColumn = () => {
	props.column.order_by = !props.column.order_by
		? 'asc'
		: props.column.order_by == 'asc'
		? 'desc'
		: null
	query.updateColumn.submit({ column: props.column })
}
</script>
