<script>
  import { createEventDispatcher } from 'svelte';

  //Propsit
  export let valittuTapahtuma = {
    id: null,
    name: '',
    date: '',
    description: '',
  };
  export let muokkaus = false;

  //Lähettää tapahtumat
  const dispatch = createEventDispatcher();

  let name = valittuTapahtuma.name;
  let date = valittuTapahtuma.date;
  let description = valittuTapahtuma.description;

  // Päivitetään lomakkeen kentät aina, kun valittuTapahtuma muuttuu
  $: if (valittuTapahtuma.id !== null) {
    name = valittuTapahtuma.name;
    date = valittuTapahtuma.date;
    description = valittuTapahtuma.description;
  }

  function handleSubmit() {
    if (name && date && description) {
      dispatch('submit', { id: valittuTapahtuma.id, name, date, description });
      resetForm();
    } else {
      alert('Täytä kaikki kentät!');
    }
  }

  function resetForm() {
    name = '';
    date = '';
    description = '';
  }
</script>

<form on:submit|preventDefault={handleSubmit}>
  <h2>{muokkaus ? 'Muokkaa tapahtumaa' : 'Lisää uusi tapahtuma'}</h2>
  <input type="text" bind:value={name} placeholder="Tapahtuman nimi" />
  <input type="date" bind:value={date} placeholder="Päivämäärä" />
  <textarea bind:value={description} placeholder="Kuvaus"></textarea>
  <button type="submit"
    >{muokkaus ? 'Tallenna muutokset' : 'Lisää tapahtuma'}</button
  >
</form>

<style>
  form {
    display: flex;
    flex-direction: column;
  }
  input,
  textarea {
    margin-bottom: 10px;
    pointer-events: auto;
  }
  h2 {
    color: orange;
  }
</style>
