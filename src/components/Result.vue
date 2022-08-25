<template>
    <transition name="fade">
        <div class="result">
            <div class="title">{{ results[resultIndex].title }}</div>
            <div class="desc">
                {{ results[resultIndex].desc }}
            </div>
        </div>
    </transition>
</template>

<script>export default {
    name: "Result",
    props: ["totalCorrect", "results"],
    computed: {
        resultIndex() {
            let index = 0;
            this.results.forEach((item, i) => {
                if (item.min <= this.totalCorrect && item.max >= this.totalCorrect) {
                    index = i
                }
            })
            return index
        }
    }
}</script>