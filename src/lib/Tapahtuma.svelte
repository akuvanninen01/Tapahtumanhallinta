<script>
  export let tapahtuma;
  export let onMuokkaa;
  export let onPoista;
</script>

<div class="event-item">
  <h3>{tapahtuma.name}</h3>
  <p>{tapahtuma.date}</p>
  <p>{tapahtuma.description}</p>
  <button on:click={() => onMuokkaa(tapahtuma.id)}>Muokkaa</button>
  <button on:click={() => onPoista(tapahtuma.id)}>Poista</button>
</div>

<style>
  .event-item {
    border: 1px solid #ccc;
    padding: 1em;
    margin: 1em 0;
    border-radius: 5px;
    transition: transform 0.2s;
  }
  .event-item:hover {
    transform: scale(1.05);
  }
  button {
    margin-right: 10px;
  }
</style>
