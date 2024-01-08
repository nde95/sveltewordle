<script>
    import { words as WordList} from "./words.js"
    import { onMount } from 'svelte';

    let letterGuesses = Array(5).fill(""); // Array to store user input for letter guesses
    let letterStates = Array(5).fill(null); // Store state for each letter (correct position, correct letter, or incorrect)
    // let guessArray = Array(5).fill(letterGuesses) // Array to store multiple guess
    let word 

    onMount(() => {
      word = GetNewWord()
    })

    function GetNewWord() {
      const randomWordIndex = Math.floor(Math.random() * WordList.length)
      return WordList[randomWordIndex]
    } 

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

  function handleSubmit(index) {
    const playerGuess = letterGuesses.join('')
    const wordSplit = word.split('')

    let correctLetters = 0
    let correctPositions = 0

    if (playerGuess.length !== wordSplit.length) {
        alert("guess is not long enough")
        return
    }
    
    for (let i = 0; i < playerGuess.length; i++) {
      if (wordSplit[i] == playerGuess[i]) {
        letterStates[i] = 'correctPosition';
        correctPositions++;
      } else if (wordSplit.includes(playerGuess[i])) {
        letterStates[i] = 'correctLetter';
        correctLetters++;
      } else {
        letterStates[i] = 'incorrect';
      }
}
    
    if (correctPositions == 5) {
        alert("you guessed the word correctly")
    }
    

    console.log("answer includes:", correctletters, "correct letters")
    console.log("answer includes:", correctPositions, "correct positions")
  }

</script>
  
  <div class="game-container">
    <h1 class="title">
      Welcome to wordle
    </h1>
    <div class="guess-container">
      {#each letterGuesses as guess, index (index)}
      <div class="guess-slot" class:correct-position={letterStates[index] === 'correctPosition'} class:correct-letter={letterStates[index] === 'correctLetter'} class:incorrect={letterStates[index] === 'incorrect'}>
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
    <button class="grid" on:click={handleSubmit}>
        Ent
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

    .correct-position {
      background-color: green;
    }

    .correct-letter {
      background-color: yellow;
    }

    .incorrect {
      background-color: grey;
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
        margin: 2px;
        border-radius: 5px;
        box-sizing: border-box;
    }

    p {
        color: black;
    }
</style>