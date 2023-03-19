<script>
  function applySound(sound){
    const audio = new Audio();
    audio.src = 'assets/sonidos/note' + sound + '.wav';
    audio.load();
    audio.play();
}
</script>

<main>
  <div class="row">
    <div class="col-lg-6">
      <div class="list-group">
        <div on:click={() => applySound(1)} class="list-group-item list-group-item-action" style="background-color: yellow;"></div>
        <div on:click={() => applySound(2)} class="list-group-item list-group-item-action" style="background-color: orange;"></div>
        <div on:click={() => applySound(3)} class="list-group-item list-group-item-action" style="background-color: red;"></div>
        <div on:click={() => applySound(4)} class="list-group-item list-group-item-action" style="background-color: blue;"></div>
        <div on:click={() => applySound(5)} class="list-group-item list-group-item-action" style="background-color: purple;"></div>
        <div on:click={() => applySound(6)} class="list-group-item list-group-item-action" style="background-color: green;"></div>
        <div on:click={() => applySound(7)} class="list-group-item list-group-item-action" style="background-color: teal;"></div>
      </div>
    </div>
  </div>
</main>

<style>
  .list-group-item {
    cursor: pointer;
    height: 50px;
  }
  .row {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
  }
  .list-group-item:active{
    opacity: 0.7;
  }
  main{
    background-color: black;
  }
</style>