<template>
	<div class="slides">
		<app-size-form/>
		<div
			class="slides--inner"
			:style="{
				width: singleWidth*slides.length + 'px',
				marginLeft: '-' + slideInnerMarginLeft + 'px'
			}"
		>
			<app-slide
				v-for="(slide, index) in slides"
				:style="{ width: singleWidth/itemsPerSlide + 'px ' }"
				:slide="slide"
				:key="index"
			/>
		</div>
		<div class="actions">
			<span @click="prev">Prev</span>
			<span
				class="action--number"
				:class="[index === currentIndex ? 'active' : '']"
				v-for="(slide, index) in slides"
				:key="index"
				@click="goToSlide(index)"
				>{{ index + 1 }}</span
			>
			<span @click="next">Next</span>
		</div>
	</div>
</template>

<script>
import AppSlide from "@/components/Slide";
import AppSizeForm from "@/components/SizeForm";
export default {
	props: {
		itemsPerSlide: {
			type: null,
			default: 1
		}
	},
	data() {
		return {
			innerWidth: 0,
		
			currentIndex: 0
		};
	},
	methods: {
		prev() {
			if (this.currentIndex === 0) return;
			this.currentIndex--;
		},
		next() {
			if (this.currentIndex === this.slides.length - 1) return;
			this.currentIndex++;
		},
		goToSlide(index) {
			this.currentIndex = index;
		}
	},
	computed: {
		slideInnerMarginLeft() {
			return this.currentIndex * this.singleWidth;
		},
		slides:{
			get(){
				return this.$store.getters.getSlides;
			}
		},
		singleWidth:{
			get(){
				return this.$store.getters.getWidth;
			}
		}
	
	},
	components: {
		AppSlide,
		AppSizeForm,
	},
	mounted() {
		this.$nextTick(() => {

		});
	}
};
</script>

<style scoped>

span {
	cursor: pointer;
}

.slides {
	overflow: hidden;
	text-align: center;
}

.slide--inner {
	transition: margin 0.6s ease-out;
}

.actions {
	margin: 10px 0 0 0;
}

.action--number {
	margin: 0 5px;
	background-color: #fff;
	padding: 0 5px;
	border: 1px solid #000;
	cursor: pointer;
}

.action--number.active {
	color: #fff;
	background: #000;
}
</style>
