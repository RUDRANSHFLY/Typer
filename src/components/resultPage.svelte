<script>
    export let wpm = 0 ;
    export let accuracy = 0 ;
</script>




<div>
    <h1>
        Results are here ✨✨✨
    </h1>
    <p class="wpm">
        {wpm} wpm
    </p>
    <p class="acc">
        {accuracy} %
    </p>
    <a href="/">Take the test again</a>
</div>

<style>
    h1{
        font-style: italic;
        font-size: 60px;
    }
    .wpm{
        font-family: cursive;
        font-size: 50px;
    }
    .acc{
        font-family: cursive;
        font-size: 50px;
    }
    a{
        margin-top: 50px;
        letter-spacing: 5px;
        color :azure;
        font-size: 30px;
    }
</style>