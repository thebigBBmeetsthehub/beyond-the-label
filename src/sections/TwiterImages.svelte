<script>
    import { fly } from 'svelte/transition';

    const image1 = '/assets/charliekirkpost.png';
    const image2 = '/assets/twitterpost2.png';   
    const image3 = '/assets/twitterpost.png';   

    const transitionDuration = 8500; 
    const flyAmount = 200; 
</script>

<style>
    .animation-container {
        position: relative;
        width: 100%; /* Or a fixed width */
        height: 800px; /* Adjust as needed to contain all images */
        overflow: hidden; /* Hide parts of images during transition */
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .image-wrapper {
        position: absolute;
        max-width: 40%; /* Adjust size as needed */
        max-height: 40%; /* Adjust size as needed */
        object-fit: contain; /* Ensures the image fits within its bounds */
    }

    /* Positioning for each image */
    .image-1 {
        top: 10%; /* Adjust vertical position */
        right: 5%; /* Stays on the right */
        transform: rotate(3deg); /* Slightly lopsided */
        z-index: 3; /* Ensure order if overlapping */
    }

    .image-2 {
        top: 40%; /* Adjust vertical position */
        left: 5%; /* Stays on the left */
        transform: rotate(-5deg); /* Slightly lopsided */
        z-index: 2;
    }

    .image-3 {
        bottom: 5%; /* Adjust vertical position */
        /* To keep it in the middle, use left/right auto or flexbox in parent */
        left: 50%;
        transform: translateX(-60%) rotate(2deg); /* Center and slightly lopsided */
        z-index: 1;
    }
</style>

<div class="animation-container">
    <img
        src="{image1}"
        alt="Charlie Kirk Post"
        class="image-wrapper image-1"
        in:fly="{{ x: flyAmount, duration: transitionDuration }}"
    />

    <img
        src="{image2}"
        alt="Mark Kern Post"
        class="image-wrapper image-2"
        in:fly="{{ x: -flyAmount, duration: transitionDuration + 2000 }}"
    />

    <img
        src="{image3}"
        alt="Braveen Post"
        class="image-wrapper image-3"
        in:fly="{{ y: flyAmount, duration: transitionDuration + 3000 }}"
    />
</div>