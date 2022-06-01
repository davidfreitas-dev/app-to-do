<template>
    <div class="progress">
        <div class="progress-bar" :style="{ width: progress + '%' }">
                       
        </div>
        <div class="progress-value">
            <span>{{ progress }}%</span>
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

<style>
	.progress {
        position: relative;
		width: 65%;
		height: 40px;
		border: 2px solid var(--primary);
        border-radius: 5px;
		margin-top: 1rem;
        display: flex;
        flex-direction: column;
        align-items: center;
	}

	.progress-bar {
        position: absolute;
		background-color: var(--primary);
		height: 100%;
		font-weight: 600;
        align-self: flex-start;
	}

    .progress-value {
        z-index: 1;
        height: 100%;
        font-size: 1.2rem;
        display: flex;
        justify-content: center;        
        align-items: center;
        text-shadow: 1px 1px 3px #666;
    }

    @media screen and (max-width: 768px) {
        .progress {
            width: 75%;
        }
    }

    @media screen and (max-width: 550px) {
        .progress {
            width: 89%;
        }
    }
</style>