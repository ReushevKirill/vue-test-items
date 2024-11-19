<template>
	<div class="app">
		<div class="cart">
			<div class="cart-top">
				<div class="cart-top__left">
					<template v-if="itemsLeftSelected.length !== 0">
						<div
							class="cart-top__left-items"
							v-if="itemsLeftSelected.length !== 0"
						>
							<div
								class="cart-item"
								v-for="item in itemsLeftSelected"
								:key="item.id"
								@click="deleteLeftSelectedItem(item.id)"
							>
								{{ item.name }}
							</div>
						</div>
						<span
							>selected: {{ itemsLeftSelected.length }} /
							{{ maxLeftSelected }}</span
						>
					</template>
					<template v-else>
						<span class="cart-item-empty">left items is not selected</span>
					</template>
				</div>
				<div class="cart-top__right-item" @click="deleteRightSelectedItem">
					<template v-if="itemRightSelected">
						<span>{{ itemRightSelected.name }}</span>
					</template>
					<template v-else>
						<span class="cart-item-empty">right item is not selected</span>
					</template>
				</div>
			</div>
			<div class="cart-bottom">
				<div class="cart-bottom__left">
					<div class="cart-bottom__left-items">
						<div
							:class="[
								`cart-item`,
								{
									'cart-item--active': isLeftItemSelected(item.id),
								},
							]"
							v-for="item in itemsLeft"
							:key="item.id"
							@click="toggleLeftItem(item)"
						>
							{{ item.name }}
						</div>
					</div>
				</div>
				<div class="cart-bottom__right">
					<div class="cart-bottom__right-items">
						<div
							class="cart-item"
							v-for="item in itemsRight"
							:key="item.id"
							@click="selectRightItem(item)"
						>
							{{ item.name }}
						</div>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script lang="ts" setup>
import { ref } from 'vue'

interface Item {
	id: number
	name: string
}

const maxLeftSelected = ref<number>(6)

const itemsLeft = ref<Item[]>([
	{
		id: 1,
		name: 'Shoes 1',
	},
	{
		id: 2,
		name: 'Shoes 2',
	},
	{
		id: 3,
		name: 'Shoes 3',
	},
	{
		id: 4,
		name: 'Shoes 4',
	},
	{
		id: 5,
		name: 'T-shirt 1',
	},
	{
		id: 6,
		name: 'T-shirt 2',
	},
	{
		id: 7,
		name: 'T-shirt 3',
	},
	{
		id: 8,
		name: 'T-shirt 4',
	},
])

const itemsRight = ref<Item[]>([
	{
		id: 11,
		name: 'Jacket 1',
	},
	{
		id: 12,
		name: 'Jacket 2',
	},
	{
		id: 13,
		name: 'Jacket 3',
	},
	{
		id: 14,
		name: 'Jacket 4',
	},
	{
		id: 15,
		name: 'Hoodie 1',
	},
	{
		id: 16,
		name: 'Hoodie 2',
	},
	{
		id: 17,
		name: 'Hoodie 3',
	},
	{
		id: 18,
		name: 'Hoodie 4',
	},
])

const itemsLeftSelected = ref<Item[] | []>([])

const itemRightSelected = ref<Item | null>(null)

const toggleLeftItem = (item: Item) => {
	const index = itemsLeftSelected.value.findIndex(i => i.id === item.id)

	if (index !== -1) {
		itemsLeftSelected.value.splice(index, 1)
	} else if (itemsLeftSelected.value.length < maxLeftSelected.value) {
		itemsLeftSelected.value.push(item)
	}
}

const isLeftItemSelected = (id: number) => {
	return itemsLeftSelected.value.some(item => item.id === id)
}

const selectRightItem = (item: Item) => {
	itemRightSelected.value = item
}

const deleteLeftSelectedItem = (id: number) => {
	itemsLeftSelected.value = itemsLeftSelected.value.filter(
		item => item.id !== id
	)
}

const deleteRightSelectedItem = () => {
	if (!itemRightSelected.value) return
	itemRightSelected.value = null
}
</script>
