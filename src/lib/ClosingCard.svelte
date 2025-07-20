<script>
    let {title, title2, subtitle} = $props();
</script>

<div class="title-card">
    <div>
        <h1>{title}</h1>
        <h1>{title2}</h1>
        <p>{subtitle}</p>
    </div>
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
        opacity: 80%;
        margin: 0;
        color: white;
        text-shadow: 1px 1px 0 black;
    }

    p {
        font-size: 3rem;
        font-style: italic;
        opacity: 20%;
        margin: 0;
        color: white;
        text-shadow: 1px 1px 0 black;
    }

    @media (max-width: 800px) {
        h1 {
            font-size: 2.2rem;
        }
        p {
            font-size: 1.5rem;
        }
    }
</style>