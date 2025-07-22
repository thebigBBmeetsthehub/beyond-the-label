<script>
    let {p1, p2, p3, p4, p5, p6, p7, p8} = $props();
</script>

<div class="analysis-card">
    <div>
        <p>{p1}</p>
        <p>{p2}</p>
        <p>{p3}</p>
        <p>{p4}</p>
        <p>{p5}</p>
        <p>{p6}</p>
        <p>{p7}</p>
        <p>{p8}</p>
    </div>
</div>

<style>
    .analysis-card {
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

    p {
        font-size: 2rem;
        margin: 0;
        color: white;
        text-shadow: 1px 1px 0 black;
    }

    @media (max-width: 800px) {
        p {
            font-size: 0.5rem;
        }
    }
</style>