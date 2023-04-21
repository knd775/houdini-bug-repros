<script lang="ts">
  import { graphql } from "$houdini";

  const q1 = graphql(`
    query q1($code: String = "US") @load {
      countries(filter: { code: { eq: $code } }) {
        name
        code
        currencies
        emoji
      }
    }
  `);

  const q2 = graphql(`
    query q2 {
      country(code: "US") {
        code
        name
      }
    }
  `);

  const q3 = graphql(`
    query q3 {
      country(code: "US") {
        code
        name
        currencies
      }
    }
  `);

  $: console.log("q1", $q1.data);
</script>

<div>
  <h3>query 1</h3>
  <pre>
    {JSON.stringify($q1.data, null, 2)}
  </pre>
</div>

<div>
  <h3>query 2</h3>
  <pre>
    {JSON.stringify($q2.data, null, 2)}
  </pre>
  <button on:click={() => q2.fetch()}>Run</button>
</div>

<div>
  <h3>query 3</h3>
  <pre>
    {JSON.stringify($q3.data, null, 2)}
  </pre>
  <button on:click={() => q3.fetch()}>Run</button>
</div>
