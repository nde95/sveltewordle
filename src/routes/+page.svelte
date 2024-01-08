<script>
    let letterGuesses = Array(5).fill(""); // Array to store user input for letter guesses
    let word = "apple"; // The word to guess

    function handleLetterClick(letter) {
    const emptyIndex = letterGuesses.indexOf("");
    if (emptyIndex !== -1) {
      letterGuesses[emptyIndex] = letter;
    }
}

    function handleBackspace() {
    const currentIndex = letterGuesses.indexOf("");
    if (currentIndex !== -1) {
      letterGuesses[currentIndex -1] = "";
    } else {
        letterGuesses[letterGuesses.length - 1] = ""
    }
  }

  </script>
  
  <div class="game-container">
    <h1 class="title">
      Welcome to wordle
    </h1>
    <div class="guess-container">
      {#each letterGuesses as guess, index (index)}
        <div class="guess-slot">
          <p class="letter-guess">
            {guess}
          </p>
        </div>
      {/each}
    </div>
    <div class="keyboard-container">
    {#each "qwertyuiop" as letter}
        <button class="grid" on:click={() => handleLetterClick(letter)}>
          {letter}
        </button>
    {/each}
    {#each "asdfghjkl" as letter}
      <button class="grid" on:click={() => handleLetterClick(letter)}>
        {letter}
      </button>
    {/each}
    {#each "zxcvbnm" as letter}
    <button class="grid" on:click={() => handleLetterClick(letter)}>
      {letter}
    </button>
    {/each}
    <button class="grid" on:click={handleBackspace}>
        Del
    </button>
    </div>
  </div>


<style>
    .game-container {
        size: fill;
        display: grid;
        grid-template-rows: auto auto;
        justify-content: center;
    }

    .guess-slot {
        border: solid;
        border-color: black;
        text-align: center;
        height: 75px;
        width: 75px;
        box-sizing: border-box;
    }

    .letter-guess {
        font-size: 20px;
    }

    .guess-container {
        display: grid;
        grid-template-columns: repeat(5, 1fr);
        margin-bottom: 20px;
        justify-items: center;
    }

    .keyboard-container {
        display: grid;
        grid-template-columns: repeat(10, 1fr);
        
    }

    .title {
        text-align: center;
    }

    .grid {
        background-color: #e0ded7;
        padding: 10px;
        text-align: center;
        margin: 5px;
        border-radius: 5px;
        box-sizing: border-box;
    }

    p {
        color: black;
    }
</style>