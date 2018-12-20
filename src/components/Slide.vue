<template>
	<div class="slide"><img :src="slide.src" alt="" /></div>
</template>

<script>
export default {
	props: ["slide"],
	data() {
		return {};
	}
};
</script>

<style scoped>
img {
	max-width: 100%;
}
.slide {
	display: inline-block;
}
</style>
