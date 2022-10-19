<script setup lang="ts">
import * as accordion from '@zag-js/accordion'
import { normalizeProps, useMachine } from '@zag-js/vue'
import { computed } from 'vue'

const data = [
	{ title: 'Watercraft', content: 'Sample accordion content' },
	{ title: 'Automobiles', content: 'Sample accordion content' },
	{ title: 'Aircrafts', content: 'Sample accordion content' },
]

const [state, send] = useMachine(accordion.machine({ id: '1' }))

const api = computed(() => accordion.connect(state.value, send, normalizeProps))
</script>

<template>
	<div ref="ref" v-bind="api.rootProps">
		<div
			v-for="item in data"
			:key="item.title"
			v-bind="api.getItemProps({ value: item.title })"
		>
			<h3>
				<button
					v-bind="api.getTriggerProps({ value: item.title })"
					class="flex justify-between items-center p-5 w-full font-medium text-left text-gray-500 rounded-t-xl border border-b-0 border-gray-200 focus:ring-4 focus:ring-gray-200 dark:focus:ring-gray-800 dark:border-gray-700 dark:text-gray-400 hover:bg-gray-100 dark:hover:bg-gray-800"
				>
					{{ item.title }}
					<svg
						data-accordion-icon
						class="w-6 h-6 shrink-0"
						:class="{ 'rotate-180': api.value == item.title }"
						fill="currentColor"
						viewBox="0 0 20 20"
						xmlns="http://www.w3.org/2000/svg"
					>
						<path
							fill-rule="evenodd"
							d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z"
							clip-rule="evenodd"
						></path>
					</svg>
				</button>
			</h3>
			<div
				v-bind="api.getContentProps({ value: item.title })"
				class="p-5 border border-b-0 border-gray-200 dark:border-gray-700 dark:bg-gray-900"
			>
				{{ item.content }}
			</div>
		</div>
	</div>
</template>
