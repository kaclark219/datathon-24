<script>
    import '../../style/style.css';
    import white_circle from '$lib/assets/White_Circle.svg';
    import logo from '$lib/assets/mimc-logo-circle.png';
    import WordSearch from '$lib/WordSearch.svelte'
</script>

<div class="top-bar">
    <div class="website-name">
        <img src={logo} alt="circle logo">
        <a href="./"><h1 class="app-name">Make It Make Cents</h1></a>
    </div>
    <div class="user">
        <img src={white_circle} alt="profile">
        <p class="hello-user">Hi, Bailey!</p>
        <div class="drop-down">&gt;</div>
    </div>
</div>

<div class="dash">
    <h2>Vocab Word Search</h2>
    <WordSearch />
    
    <style>
        .dash {
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
        }
        h2 {
            margin-top: 20px;
            color: #006D1F;
            font-family: "Press Start 2P";
            font-size: 24px;
            margin-bottom: 20px;
        }
        :global(*) {
            box-sizing: border-box;
            padding: 0;
            margin: 0;
        }
    
        :global(body) {
            color: hsl(206, 53%, 94%);
            background: hsl(222, 22%, 9%);
        }
    </style>
</div>

