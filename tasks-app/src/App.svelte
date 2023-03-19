<script>
  import Navbar from "./components/Navbar.svelte";
  import Tasks from "./components/Task.svelte";

</script>

<main class="wallpaper">
  <Navbar />
  <Tasks />
</main>

<style>
  .wallpaper{
    background-image: url('../assets/mountain.jpg');
    height: 100vh;
    background-position: center;
    background-size: cover;
}
</style>
