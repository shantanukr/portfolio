<script context="module">
  import { client } from '$lib/graphql-client'
  import { authorsQuery, projectsQuery } from '$lib/graphql-queries'

  export const load = async () => {

    const [authorReq, projectsReq] = await Promise.all([
      client.request(authorsQuery),
      client.request(projectsQuery),
    ])

    const { authors } = authorReq
    const { projects } = projectsReq

    return {
      props: {
        projects,
        authors,
      },
    }
  }
</script>


<script>
  export let projects
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
  <button class="btn btn-outline btn-primary mr-10">My Projects</button>
  <button class="btn btn-outline btn-primary">Contact Me</button>
</div>