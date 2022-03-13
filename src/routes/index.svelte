<script context="module">
  import { client } from '$lib/graphql-client'
  import { authorsQuery } from '$lib/graphql-queries'

  export const load = async () => {

    const [authorReq] = await Promise.all([
      client.request(authorsQuery)
    ])

    const { authors } = authorReq

    return {
      props: {
        authors,
      },
    }
  }
</script>


<script>
  export let authors
</script>

<svelte:head>
  <title>My Portfolio project</title>
</svelte:head>

<h1 class="font-bold text-center mb-20 text-5xl"> Welcome to my Portfolio </h1>

{#each authors as { name, intro, picture: { url } }}
  <div class="flex mb-35 items-end">
    <div class="mr-6">
      <h2 class="text-3xl mb-4 font-bold tracking-wider">{name}</h2>
      <p class="text-xl mb-4">{intro}</p>
    </div>
  </div>
{/each}

<div>
  <a class="btn btn-outline btn-primary mr-10" href="/projects">My projects</a>
  <a class="btn btn-outline btn-primary mr-10" href="/contacts">Contact Me</a>
</div>