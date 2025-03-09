<script lang="ts">
    interface Props {
        videoid: string;
        customer: string;
        poster?: string;
        params?: string | { [x: string]: any }
        title?: string;
    }

    let { videoid, customer, poster, params, title, ...other }: Props = $props();

    let a = $state(false);

    let s = $derived(poster || `https://customer-${customer}.cloudflarestream.com/${videoid}/thumbnails/thumbnail.jpg`);

    let p = $derived(params ? (typeof params === 'string' ? params : new URLSearchParams(params).toString()) : '')

    async function c(event: MouseEvent) {
        if (!(event.metaKey || event.ctrlKey)) {
            event.preventDefault();
            a = true;
        }
    }
	
    $effect(() => {
        let { head } = document;
        for (let url of [
            `https://customer-${customer}.cloudflarestream.com`,
        ]) if (!head.querySelector(`link[href="${url}"]`)) {
            head.append(Object.assign(document.createElement('link'), { rel: 'preconnect', href: url }));
        }
    });
</script>

<a 
    href="https://customer-{customer}.cloudflarestream.com/{videoid}/iframe?autoplay=true{p && `&${p}`}"
    target="_blank"
    rel="noopener noreferrer"
    aria-label={title}
    {title} 
    style={`background-image: url('${s}');`}
    onclick={c}
    {...other}
    class="cloudstream"
>
    {#if a}
        <iframe 
            src="https://customer-{customer}.cloudflarestream.com/{videoid}/iframe?autoplay=true{p && `&${p}`}" 
            aria-label={title}
            {title} 
            width="720"
            height="405"
            frameborder="0" 
            allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
            allowfullscreen
            loading="lazy"
        ></iframe>
    {:else}
        <button tabindex="-1" type="button" aria-label="button">
            <svg viewBox="0 0 48 48" fill="none" xmlns="http://www.w3.org/2000/svg"><path d="M39.72 22.26L15.72 10.26C15.12 9.95997 14.4 9.98997 13.83 10.35C13.26 10.71 12.9 11.34 12.9 12L12.9 36C12.9 36.69 13.26 37.29 13.83 37.65C14.13 37.83 14.49 37.95 14.85 37.95C15.15 37.95 15.45 37.89 15.72 37.74L39.72 25.74C40.38 25.41 40.8 24.75 40.8 24C40.8 23.25 40.38 22.59 39.72 22.26Z" fill="currentColor"></path></svg>
        </button>
    {/if}
</a>

<style>
    :global(.cloudstream) {
        aspect-ratio: 16 / 9;
        width: 100%;
        max-width: 720px;
        align-items: center;
        justify-content: center;
        display: block;
        overflow: hidden;
        position: relative;
        contain: content;
        background-position: center center;
        background-size: cover;
        text-decoration: none;
        cursor: pointer;
    }

    :global(.cloudstream > button) {
        display: block;
        position: absolute;
        transform: translate3d(-50%, -50%, 0);
        top: 50%;
        left: 50%;
        height: 5rem;
        width: 5rem;
        border-radius: 9999px;
        display: flex;
        justify-content: center;
        align-items: center;
        text-align: center;
        color: white;
        transition: background-color 0.02s linear;
        cursor: pointer;
        border: 0 !important;
        outline: 0 !important;
        background-color: transparent;
    }

    :global(.cloudstream > button > svg) {
        height: 4rem;
        width: 4rem;
        color: inherit;
        display: flex;
    }

    :global(.cloudstream:focus > button),
    :global(.cloudstream:hover > button),
    :global(.cloudstream > button:focus) {
        background-color: rgba(255, 255, 255, 0.25);
        opacity: 1;
    }

    :global(.cloudstream > iframe) {
        width: 100%;
        height: 100%;
        position: absolute;
        inset: 0;
        border: 0;
    }
</style>