<script>
    import PreviewBox from './lib/PreviewBox.svelte';

  let name = $state('');
  let rMin = $state('0');
  let rMax = $state('255');
  let gMin = $state('0');
  let gMax = $state('255');
  let bMin = $state('0');
  let bMax = $state('255');
  let error = $state('');

  let colorRange = $derived({
      name,
      rMin,
      rMax,
      gMin,
      gMax,
      bMin,
      bMax,
  });

  const submit = (event) => {
    event.preventDefault();

    // manual instead of w/ JSON.stringify to retain formating & trailing comma
    const text = `{
      name: ${name},
      rMin: ${rMin},
      rMax: ${rMax},
      gMin: ${gMin},
      gMax: ${gMax},
      bMin: ${bMin},
      bMax: ${bMax},
    }`;
    copyToClipboard(text);
  }

  async function copyToClipboard(text) {
    try {
      await navigator.clipboard.writeText(text);
      error = '';
    } catch (err) {
      error = 'Error copying, check console.';
      console.error('Failed to copy text: ', err);
    }
  }
</script>

<main>
  <form onsubmit={submit}>
    <label>Name
      <input type="text" bind:value={name} />
    </label>
    <br />
    <label>Red Min
      <input type="range" min="0" max="255" bind:value={rMin} />
    </label>
        <label>Red Max
      <input type="range" min="0" max="255" bind:value={rMax} />
    </label>

    <hr />
    <label>Green Min
      <input type="range" min="0" max="255" bind:value={gMin} />
    </label>
    <label>Green Max
      <input type="range" min="0" max="255" bind:value={gMax} />
    </label>

    <hr />
    <label>Blue Min
      <input type="range" min="0" max="255" bind:value={bMin} />
    </label>
    <label>Blue Max
      <input type="range" min="0" max="255" bind:value={bMax} />
    </label>
    <br />
    <button type="submit">Copy to Clipboard</button>
  </form>

  {#if error}
    <p>{error}</p>
  {/if}

  <div class="preview-grid">
    <PreviewBox label="mid-high" {colorRange} />
    <PreviewBox label="mid" {colorRange} />
    <PreviewBox label="mid-low" {colorRange} />
    <PreviewBox label="Rgb" {colorRange} />
    <PreviewBox label="rGb" {colorRange} />
    <PreviewBox label="rgB" {colorRange} />
    <PreviewBox label="RGb" {colorRange} />
    <PreviewBox label="rGB" {colorRange} />
    <PreviewBox label="RGB" {colorRange} />
  </div>
</main>

<style>
  form {
    margin-bottom: 1.5rem;
  }
.preview-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: repeat(3, 1fr);
  grid-column-gap: 0px;
  grid-row-gap: 0px;
}
</style>
