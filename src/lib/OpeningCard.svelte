<script>
    import { fade, fly } from "svelte/transition";
    let {title, title2} = $props();
    let titleCardIsVisible = $state(true);

    const options = {
        threshold: 0.1,
    };

    const observeTitleCard = (entries) => {
        entries.forEach((entry) => {
            if (entry.intersectionRatio < 0.1) {
                titleCardIsVisible = false;
            } else {
                titleCardIsVisible = true;
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
</script>

<div
    class="title-card"
    use:observe={observeTitleCard}
    in:fly={{y: 200, duration: 2000}}
    out:fade>
    {#if titleCardIsVisible}
        <div class="content">
            <h1>{title}</h1>
            <h1>{title2}</h1>
        </div>
    {/if}
</div>

<style>
    .title-card {
        background-color: #353142;
        height: 100vh;
        display: flex;
        justify-content: center;
        align-items: center;
        text-align: center;
        padding: 2rem;
        box-sizing: border-box;
        font-family: "Inter", sans-serif;
    }

    h1 {
        font-size: 3rem;
        opacity: 20%;
        margin: 0;
        color: white;
        text-shadow: 1px 1px 0 black;
    }

    @media (max-width: 800px) {
        h1 {
            font-size: 2.2rem;
        }
    }
</style>