<script>
    import '../../style/style.css';
    import white_circle from '$lib/assets/White_Circle.svg';
    import logo from '$lib/assets/mimc-logo-circle.png';
    import cover from '$lib/assets/mimc-logo.png'
    import SingleCard from '$lib/SingleCard.svelte'
    import atm from '$lib/assets/atm.png'
    import bank from '$lib/assets/bank.png'
    import check from '$lib/assets/check.png'
    import coins from '$lib/assets/coins.png'
    import debit_card from '$lib/assets/debit_card.png'
    import dollar_bills from '$lib/assets/dollar_bills.png'
            
    let imgCover = cover
    let imgATM = atm
    let imgBank = bank
    let imgCheck = check
    let imgCoins = coins
    let imgCard = debit_card
    let imgBills = dollar_bills
        
    const cardImages = [
        { src: imgATM, matched: false },
        { src: imgBank, matched: false },
        { src: imgCheck, matched: false },
        { src: imgCoins, matched: false },
        { src: imgCard, matched: false },
        { src: imgBills, matched: false },
    ]
        
    let cards = []
    let turns = 0
    let choiceOne = null
    let choiceTwo = null
    let disabled = false

    const shuffledCards = () => {
        const shuffledCards = [...cardImages, ...cardImages]
        .sort(() => Math.random() - 0.5)
        .map((card) => ({ ...card, id: Math.random()}))
        cards = shuffledCards
        turns = 0
    }

    const handleChoice = card => {
        choiceOne ? choiceTwo = card : choiceOne = card
    }

    $: if (choiceOne && choiceTwo) {
        disabled = true
        if (choiceOne.src === choiceTwo.src) {
            console.log('those cards match')
            cards = cards.map(card => {
                if (card.src === choiceOne.src) {
                    return { ...card, matched: true }
                } else {
                    return card
                }
            })
            resetTurn()
        } else {
            console.log('those cards do not match')
            setTimeout(() => resetTurn(), 1000)
        }
    }
            
    $: console.log(cards)

    $: shuffledCards()

    const resetTurn = () => {
        choiceOne = null
        choiceTwo = null
        turns = turns + 1
        disabled = false
    }
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
    <div class="App">
        <h2>Card Matching</h2>
        <button on:click={shuffledCards}>
            New Game
        </button>
        <div class="card-grid">
        {#each cards as card (card.id)}
            <SingleCard
                {card}
                {imgCover}
                {disabled}
                {handleChoice}
                flipped={
                    card === choiceOne ||
                    card === choiceTwo ||
                    card.matched} />
        {/each}
        </div>
        <p>
            Turns: {turns}
        </p>
    </div>
</div>

<style>
    .dash {
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
    }
    .App {
        margin: 0 auto;
        min-height: 100vh;
        text-align:center;
        padding: 1rem;
        color: #006D1F;
        font-family: "Open Sans";
    }
    p {
        font-weight: 600;
        margin-top: 10px;
    }
    h2 {
        margin-top: 20px;
        color: #006D1F;
        font-family: "Press Start 2P";
        font-size: 24px;
        margin-bottom: 20px;
    }
    button {
        background-color: #0320B4;
        color: white;
        text-align: center;
        font-family: "Open Sans";
        font-size: 24px;
        font-weight: 600;
        padding: 10px 30px;
        border-radius: 10px;
        &:hover, &:focus {
            background-color: #001685;
        }
    }
    .card-grid {
        margin-top: 20px;
        display: grid;
        grid-template-columns: repeat(4, 1fr);
        grid-gap: 10px;
    }
</style>