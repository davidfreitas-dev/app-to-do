<template>
    <div class="wrapper">
        <div class="progress">
            <div class="progress__bar" :style="{ width: progress + '%' }"></div>
            <span class="progress__value">{{ progress }}%</span>
        </div>
    </div>
</template>

<script>
export default({
    props: {
        progress: { type: Number, default: 0 }
    }    
})
</script>