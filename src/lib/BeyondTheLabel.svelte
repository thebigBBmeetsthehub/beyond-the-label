<script>
    import { fade, fly } from "svelte/transition";
    import { onMount, onDestroy } from 'svelte';

    let { mainText, subText } = $props();
    let unseenClimbIsVisible = $state(false);
    let scrollProgressInSection = $state(0);
    let stigmaTokenOpacity = $state(0);
    let stigmaCulturalFitOpacity = $state(0);
    let sectionElement;

    const options = {
        threshold: 0.1,
        rootMargin: '0px 0px -20% 0px'
    };

    const observeUnseenClimbSection = (entries) => {
        entries.forEach((entry) => {
            if (entry.isIntersecting && entry.intersectionRatio >= 0.1) {
                unseenClimbIsVisible = true;
            } else {
                unseenClimbIsVisible = false;
            }
        });
    };

    function observe(node, callback, options) {
        const observer = new IntersectionObserver(callback, options);
        observer.observe(node);
        return {
            destroy() {
                observer.disconnect();
            },
        };
    }

    function handleLocalScroll() {
        if (!sectionElement) return;

        const rect = sectionElement.getBoundingClientRect();
        const viewportHeight = window.innerHeight;

        const startPoint = viewportHeight * 0.2; 
        const endPoint = viewportHeight * 0.8;  

        if (rect.top < endPoint && rect.bottom > startPoint) {
            const currentPos = viewportHeight - rect.top;
            scrollProgressInSection = Math.min(1, Math.max(0, (currentPos - startPoint) / (endPoint - startPoint)));
        } else if (rect.top >= endPoint) {
            scrollProgressInSection = 0;
        } else if (rect.bottom <= startPoint) {
            scrollProgressInSection = 1;
        }

        if (unseenClimbIsVisible) {
            stigmaTokenOpacity = scrollProgressInSection > 0.3 ? Math.min(1, (scrollProgressInSection - 0.3) * 3) : 0;
            stigmaCulturalFitOpacity = scrollProgressInSection > 0.6 ? Math.min(1, (scrollProgressInSection - 0.6) * 3) : 0;
        } else {
            stigmaTokenOpacity = 0;
            stigmaCulturalFitOpacity = 0;
        }
    }

    onMount(() => {
        window.addEventListener('scroll', handleLocalScroll);

        handleLocalScroll(); 

        if (sectionElement) {
            observeUnseenClimbSection([{
                isIntersecting: sectionElement.getBoundingClientRect().top < window.innerHeight && sectionElement.getBoundingClientRect().bottom > 0,
                intersectionRatio: 0,
                boundingClientRect: sectionElement.getBoundingClientRect(),
                target: sectionElement
            }]);
        }
    });

    onDestroy(() => {
        window.removeEventListener('scroll', handleLocalScroll);
    });
</script>

<div
    class="beyond-the-label-section"
    bind:this={sectionElement}
    use:observe={[observeUnseenClimbSection, options]}
    in:fly={{y: 200, duration: 2000}}
    out:fade>
    {#if unseenClimbIsVisible}
        <div class="content">
            <h2 class="beyond-the-label-text"
                style="transform: scale({0.8 + scrollProgressInSection * 0.2});">
                {mainText}
            </h2>
            <p class="text-2xl font-light text-gray-400 mt-4"
               style="opacity: {unseenClimbIsVisible ? 1 : 0};">
                {subText}
            </p>
            <p class="stigma-word token" style="opacity: {stigmaTokenOpacity};">Token</p>
            <p class="stigma-word cultural-fit" style="opacity: {stigmaCulturalFitOpacity};">Cultural Fit</p>
        </div>
    {/if}
</div>

<style>
    .beyond-the-label-section {
        min-height: 80vh;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        padding: 4rem 2rem;
        text-align: center;
        position: relative;
        background-color: transparent;
    }

    .beyond-the-label-text {
        font-size: 8.5rem;
        font-weight: 800;
        color: #ffd970;
        text-shadow:0 0 10px rgba(245, 227, 123, 0.8);
        line-height: 1;
    }

    .stigma-word {
        position: absolute;
        font-size: 3rem;
        font-weight: 700;
        color: #e94560;
        opacity: 0;
        transition: opacity 0.5s ease-out, transform 0.5s ease-out; 
        pointer-events: none;
        text-shadow: 0 0 10px rgba(233, 69, 96, 0.5);
    }

    .stigma-word.token { bottom: 10%; left: 50%; transform: translateX(-50%); }
    .stigma-word.cultural-fit { top: 30%; left: 50%; transform: translateX(-50%); }

    @media (max-width: 768px) {
        .stigma-word {
            font-size: 2rem;
        }
        .beyond-the-label-text {
            font-size: 3rem;
        }
    }
</style>