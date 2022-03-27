<template>
    <div class="progress">
        <div class="progress-bar" :style="{width: progress + '%'}">
                       
        </div>
        <div class="progress-value">
            <span>{{ progress }}%</span>
        </div>
    </div>
</template>

<script>
export default({
    props: {
        progress: { type: Number, default: 0}
    }    
})
</script>

<style scoped>
	.progress {
        display: flex;
        flex-direction: column;
        align-items: center;
        position: relative;
		width: 50%;
		height: 40px;
		border: 2px solid var(--main);
        border-radius: 5px;
		margin-top: 1rem;
		font-weight: 700;
        color: #fff;
        text-shadow: 1px 1px 2px black;
	}

	.progress-bar {
		height: 100%;
        position: absolute;
        align-self: flex-start;
		background-color: var(--main);
	}

    .progress-value {
        z-index: 1;
        height: 100%;
        display: flex;
        justify-content: center;        
        align-items: center;
    }

    @media screen and (max-width: 768px) {
        .progress {
            width: 75%;
        }
    }

    @media screen and (max-width: 550px) {
        .progress {
            width: 85%;
        }
    }
</style>