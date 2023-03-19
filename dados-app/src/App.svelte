<script>
  
  let number1 = 1;
  let number2 = 2;

  let diceLeft = 'assets/img/dice' + number1 + '.png';
  let diceRight = 'assets/img/dice' + number2 +'.png';
  
  function rollDice(){
    number1 = Math.floor(Math.random() * 6) + 1;
    number2 = Math.floor(Math.random() * 6) + 1;

    diceLeft = 'assets/img/dice' + number1 + '.png';
    diceRight = 'assets/img/dice' + number2 +'.png';
  }

</script>

<main>
  <div class="jumbotron text-center pt-5">
    <button class="btn btn-success lg" on:click={rollDice}>Roll dice</button>
    <br>
    <img src={diceLeft} alt="Dice 1" class="img">
    <img src={diceRight} alt="Dice 2" class="img">
    {#if number1 == number2}
    <h1>
      <span class="badge text-bg-success">Winner</span>
    </h1>
    {/if}
  </div>
</main>

<style>
  main{
    background-color: black;
    height: 100vh;
  }
  .img{
    widows: 300px;
    height: 300px;
    background-color: red;
    margin: 30px;
    border-radius: 25px;
  }
</style>
