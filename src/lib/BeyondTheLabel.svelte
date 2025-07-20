<script>
    import { fade, fly } from "svelte/transition";
    import { onMount, onDestroy } from 'svelte';

    let { mainText, subText } = $props();
    let beyondTheLabelIsVisible = $state(true);
    let scrollProgressInSection = $state(0);
    let stigmaDiversityHireOpacity = $state(0);
    let stigmaLessThanOpacity = $state(0);
    let sectionElement;

    const options = {
        threshold: 0.1,
        rootMargin: '0px 0px -20% 0px'
    };

    const observeUnseenClimbSection = (entries) => {
        entries.forEach((entry) => {
            if (entry.isIntersecting && entry.intersectionRatio >= 0.1) {
                beyondTheLabelIsVisible = true;
            } else {
                beyondTheLabelIsVisible = false;
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

        if (beyondTheLabelIsVisible) {
            stigmaDiversityHireOpacity = scrollProgressInSection > 0.3 ? Math.min(1, (scrollProgressInSection - 0.3) * 3) : 0;
            stigmaLessThanOpacity = scrollProgressInSection > 0.6 ? Math.min(1, (scrollProgressInSection - 0.6) * 3) : 0;
        } else {
            stigmaDiversityHireOpacity = 0;
            stigmaLessThanOpacity = 0;
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
    {#if beyondTheLabelIsVisible}
        <div class="content">
            <h2 class="beyond-the-label-text"
                style="transform: scale({0.8 + scrollProgressInSection * 0.2});">
                {mainText}
            </h2>
            <p class="beyond-the-label-sub-text"
               style="opacity: {beyondTheLabelIsVisible ? 1 : 0};">
                {subText}
            </p>
            <p class="stigma-word diversity-hire" style="opacity: {stigmaDiversityHireOpacity};">Diversity Hire</p>
            <p class="stigma-word less-than" style="opacity: {stigmaLessThanOpacity};">Less Than</p>
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

    .beyond-the-label-sub-text {
        font-size: 2.5rem;
        font-style: italic;
        font-weight: 400;
        color: #ad9249;
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

    .stigma-word.diversity-hire { 
        bottom: 10%; 
        left: 50%; 
    }

    .stigma-word.less-than { 
        top: 30%; 
        left: 50%; 
    }

    @media (max-width: 768px) {
        .stigma-word {
            font-size: 2rem;
        }
        .beyond-the-label-text {
            font-size: 3rem;
        }
    }
</style>