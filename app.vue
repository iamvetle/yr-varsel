<template>
	<div>
	<Title>The weather in Krapfoss</Title>
		<div v-if="apiSvgUrl" id="divGuy">
			<!-- {{ apiSvgUrl }} -->
			<img :src="apiSvgUrl" id="theImg"/>

		</div>
		<div v-else>
			<p>No data yet</p>
		</div>
	</div>
</template>

<script setup lang="ts">
	const apiSvgUrl = ref<any>(null);

    const url = "https://www.yr.no/en/content/1-2715300/meteogram.svg";
	const delay = 15000;

	const intervalID = ref<any>(null);

	const fetchData = () => {
		console.debug("fetchData called from setInterval")

		apiSvgUrl.value = null
		apiSvgUrl.value = url
	};

	onMounted(async () => {
		fetchData()
    console.debug("on mounted run")
		intervalID.value = setInterval(fetchData, delay);
	});

	onUnmounted(() => {
		if (intervalID.value) {
			clearInterval(intervalID.value);
		}
	});
</script>


<style scoped>

#theImg {
	max-width: 80%;
	max-height: 100vh;
}

#divGuy {
	display: flex;
	justify-content:center;
}

@media only screen and (max-width:768px) {
	#theImg {
		width:100%;
		max-width:100%;
	};
};

</style>