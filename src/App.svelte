<script>
  import Tapahtuma from './lib/Tapahtuma.svelte';
  import Uusi from './lib/Uusi.svelte';

  let tapahtumat = [];
  let valittuTapahtuma = { id: null, name: '', date: '', description: '' };
  let muokkaus = false;

  function addEvent(event) {
    tapahtumat = [...tapahtumat, { ...event, id: Date.now() }];
  }

  function updateEvent(updatedEvent) {
    tapahtumat = tapahtumat.map((event) =>
      event.id === updatedEvent.id ? updatedEvent : event
    );
  }

  function deleteEvent(id) {
    tapahtumat = tapahtumat.filter((event) => event.id !== id);
  }

  function editEvent(id) {
    valittuTapahtuma = { ...tapahtumat.find((event) => event.id === id) };
    muokkaus = true;
  }

  function handleFormSubmit(event) {
    if (muokkaus) {
      updateEvent(event.detail);
    } else {
      addEvent(event.detail);
    }
    resetForm();
  }

  function resetForm() {
    valittuTapahtuma = { id: null, name: '', date: '', description: '' };
    muokkaus = false;
  }
</script>

<main>
  <h1>Tapahtumien suunnittelu</h1>
  <Uusi {valittuTapahtuma} {muokkaus} on:submit={handleFormSubmit} />
  {#if tapahtumat.length > 0}
    <h2>Events</h2>
    <ul>
      {#each tapahtumat as tapahtuma (tapahtuma.id)}
        <li>
          <Tapahtuma {tapahtuma} onMuokkaa={editEvent} onPoista={deleteEvent} />
        </li>
      {/each}
    </ul>
  {:else}
    <p>Ei lisättyjä tapahtumia</p>
  {/if}
</main>

<style>
  main {
    text-align: center;
    font-family: Arial, sans-serif;
  }
  ul {
    list-style: none;
    padding: 0;
  }
  li {
    margin-bottom: 10px;
  }
  h1 {
    color: blue;
  }
</style>
