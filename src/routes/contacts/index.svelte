<svelte:head>
  <title>Contact Me</title>
</svelte:head>

<script context="module">
    import { email_client } from '$lib/form-spree-client'
    const endpoint = email_client
    let name = ""
    let email = ""
    let body = ""
    let formData = {}
    async function handleSubmit() {
        formData = {
            "name": name,
            "_replyto": email,
            "message": body
        };
        const res = await fetch(endpoint, {
			method: 'POST',
			body: JSON.stringify(formData),
            headers: { "Content-Type": "application/json"}
		})
		
		const respone_json = await res.json()
        const text = await res.text();
        console.log(text)
        if (res.ok) {
            return text;
        } else {
            throw new Error(text);
        }
    };
		   
</script>

<h1 class="text-5xl m-3">Contact Me</h1>
<p class="text-xl m-3">Send me a message here, Don't worry we will not spam you 😀</p>
<div>
    <form on:submit|preventDefault={handleSubmit}>
        <input type="text" placeholder="Your Name" class="input input-bordered input-primary w-full max-w-sm m-3" bind:value={name}>
        <br>
        <input type="text" placeholder="Your Email" class="input input-bordered input-primary w-full max-w-sm m-3" bind:value={email} required>
        <br>
        <textarea class="textarea textarea-primary w-full max-w-sm m-3 h-40" placeholder="Your Message" bind:value={body} required></textarea>
        <br>
        <button class="btn btn-outline btn-primary m-3 w-96">Submit</button>
    </form>
</div>
<p class="text-xl m-3">Also find me at...</p>
<div class="avatar m-3 ">
  <div class="w-20 rounded-full bg-white">
    <a href="https://github.com/shantanukr">
        <img src="/assets/icons/github.svg" alt="My Github" />
    </a>
  </div>
</div>
<div class="avatar m-3">
  <div class="w-20 rounded-full bg-white">
    <a href="https://dev.to/shantanukr">
        <img src="/assets/icons/devto.svg" alt="My dev.to profile"/>
    </a>
  </div>
</div>
<div class="avatar m-3">
  <div class="w-20 rounded-full bg-white">
    <a href="https://www.linkedin.com/in/shantanu-481b761b6">
        <img src="/assets/icons/linkedin.svg" alt="My LinkedIn" />
    </a>
  </div>
</div>