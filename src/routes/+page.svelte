<script>
    import '../style/style.css';
    import white_circle from '$lib/assets/White_Circle.svg';
    import logo from '$lib/assets/mimc-logo-circle.png';

    let starCount = 0;
    function incrementStarCount(num) {starCount += num;}
    
    let rewardsCompleted = [false, false, false, false];
    function decrementStarCount(num, index) {
        starCount -= num;
        rewardsCompleted[index] = true;
    }

    let savings = 0.00;
    let roundedUp = [false, false, false];
    function roundUpToSavings(amount, index) {
        savings += amount;
        roundedUp[index] = true;
    }

    let goalsCompleted = [false, false];
    function goalCompleted(num, index) {
        starCount += num;
        goalsCompleted[index] = true;
    }

</script>

<div class="top-bar">
    <div class="website-name">
        <img src={logo} alt="circle logo">
        <h1 class="app-name">Make It Make Cents</h1>
    </div>
    <div class="user">
        <img src={white_circle} alt="profile">
        <p class="hello-user">Hi, Bailey!</p>
        <div class="drop-down">&gt;</div>
    </div>
</div>
<div class="dash">
    <div class="column-1">
        <div class="recent-purchases">
            <h2 class="title">Recent Purchases</h2>
            <div class="purchase-list">
                <div class="purchase">
                    <div class="bullet">&gt;</div>
                    <div class="left-purchase">
                        <h3 class="date-and-location">11/09 - Amazon.com</h3>
                        <p class="nearest-dollar" class:crossed={roundedUp[0]}>$0.17 to Nearest Dollar</p>
                    </div>
                    <div class="right-purchase">
                        <h4 class="spent">$27.83</h4>
                    <button on:click={() => roundUpToSavings(0.17,0)}>Round Up to Savings</button>
                    </div>
                </div>
                <hr class="solid">
                <div class="purchase">
                    <div class="bullet">&gt;</div>
                    <div class="left-purchase">
                        <h3 class="date-and-location">11/07 - GameStop</h3>
                        <p class="nearest-dollar" class:crossed={roundedUp[1]}>$0.82 to Nearest Dollar</p>
                    </div>
                    <div class="right-purchase">
                        <h4 class="spent">$16.18</h4>
                    <button on:click={() => roundUpToSavings(0.82,1)}>Round Up to Savings</button>
                    </div>
                </div>
                <hr class="solid">
                <div class="purchase" style="margin-bottom: 30px">
                    <div class="bullet">&gt;</div>
                    <div class="left-purchase">
                        <h3 class="date-and-location">11/02 - The LEGO Store</h3>
                        <p class="nearest-dollar" class:crossed={roundedUp[2]}>$0.48 to Nearest Dollar</p>
                    </div>
                    <div class="right-purchase">
                        <h4 class="spent">$9.52</h4>
                    <button on:click={() => roundUpToSavings(0.48,2)}>Round Up to Savings</button>
                    </div>
                </div>
            </div>
        </div>
        <div class="savings-goals">
            <h2 class="title">Savings Goals</h2>
            <div class="goal-list">
                <div class="goal">
                    <div class="left-goal">
                        <h3 class="goal-name" class:crossed={goalsCompleted[0]}>Play a Game!</h3>
                        <div class="goal-reward">
                            <p class="star-amount">1</p>
                            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 260 245">
                                <path d="m56,237 74-228 74,228L10,96h240"/>
                                </svg>
                        </div>
                    </div>
                    <button on:click={() => goalCompleted(1,0)}>Complete</button>
                </div>
                <hr class="solid">
                <div class="goal">
                    <div class="left-goal">
                        <h3 class="goal-name" class:crossed={goalsCompleted[1]}>Round Up Savings 3 Times</h3>
                        <div class="goal-reward">
                            <p class="star-amount">3</p>
                            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 260 245">
                                <path d="m56,237 74-228 74,228L10,96h240"/>
                                </svg>
                        </div>
                    </div>
                    <button on:click={() => goalCompleted(3,1)}>Complete</button>
                </div>
                <button class="new-goal">Add New Goal</button>
            </div>
        </div>
    </div>
    <div class="column-2">
        <div class="current-savings">
            <h2 class="title">Current Savings</h2>
            <div class="savings-number">
                <p class="savings-number">${savings}</p>
            </div>
        </div>
        <div class="current-stars">
            <h2 class="title">Current Stars</h2>
            <div class="current-stars-container">
                <p class="current-star-number">{starCount}</p>
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 260 245">
                    <path d="m56,237 74-228 74,228L10,96h240"/>
                    </svg>
            </div>
        </div>
        <div class="available-games">
            <h2 class="title">Available Games</h2>
            <div class="game-list">
                <div class="game">
                    <div class="game-top">
                        <div class="game-top-left">
                            <p class="star-amount">3</p>
                            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 260 245">
                                <path d="m56,237 74-228 74,228L10,96h240"/>
                                </svg>
                        </div>
                        <div class="game-top right">
                            <a href="./vocab_game"target="_blank"><button on:click={() => incrementStarCount(3)}>&gt;</button></a>
                        </div>
                    </div>
                    <div class="game-bottom">
                        <p class="game-name">Vocab Crossword</p>
                    </div>
                </div>
                <hr class="solid">
                <div class="game">
                    <div class="game-top">
                        <div class="game-top-left">
                            <p class="star-amount">1</p>
                            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 260 245">
                                <path d="m56,237 74-228 74,228L10,96h240"/>
                                </svg>
                        </div>
                        <div class="game-top right">
                            <a href="./matching_game" target="_blank"><button on:click={() => incrementStarCount(1)}>&gt;</button></a>
                        </div>
                    </div>
                    <div class="game-bottom">
                        <p class="game-name">Card Matching</p>
                    </div>
                </div>
                <hr class="solid">
            <p id="disclaimer">More games coming soon!</p>
            </div>
        </div>
    </div>
    <div class="column-3">
        <div class="rewards">
            <h2 class="title">Rewards</h2>
            <div class="reward-list">
                <div class="reward">
                    <h3 class="reward-top" class:crossed={rewardsCompleted[0]}>Two Hours of Any Video Game Time</h3>
                    <div class="reward-bottom">
                        <div class="reward-bottom-left">
                            <p class="star-amount">3</p>
                            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 260 245">
                                <path d="m56,237 74-228 74,228L10,96h240"/>
                                </svg>
                        </div>
                        <button on:click={() => decrementStarCount(3,0)}>Redeem</button>
                    </div>
                </div>
                <hr class="solid">
                <div class="reward">
                    <h3 class="reward-top" class:crossed={rewardsCompleted[1]}>Make-Your-Own Pizza Night</h3>
                    <div class="reward-bottom">
                        <div class="reward-bottom-left">
                            <p class="star-amount">5</p>
                            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 260 245">
                                <path d="m56,237 74-228 74,228L10,96h240"/>
                                </svg>
                        </div>
                        <button on:click={() => decrementStarCount(5,1)}>Redeem</button>
                    </div>
                </div>
                <hr class="solid">
                <div class="reward">
                    <h3 class="reward-top" class:crossed={rewardsCompleted[2]}>Trip to the Local Playground</h3>
                    <div class="reward-bottom">
                        <div class="reward-bottom-left">
                            <p class="star-amount">2</p>
                            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 260 245">
                                <path d="m56,237 74-228 74,228L10,96h240"/>
                                </svg>
                        </div>
                        <button on:click={() => decrementStarCount(2,2)}>Redeem</button>
                    </div>
                </div>
                <hr class="solid">
                <div class="reward">
                    <h3 class="reward-top" class:crossed={rewardsCompleted[3]}>Family Outing to Movie Theater</h3>
                    <div class="reward-bottom">
                        <div class="reward-bottom-left">
                            <p class="star-amount">8</p>
                            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 260 245">
                                <path d="m56,237 74-228 74,228L10,96h240"/>
                                </svg>
                        </div>
                        <button on:click={() => decrementStarCount(8,3)}>Redeem</button>
                    </div>
                </div>
                <hr class="solid">
                <button class="new-reward">Add New Reward</button>
            </div>
        </div>
    </div>
</div>