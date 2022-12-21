<script>
  import { getContent, isPreviewing, RenderContent } from '@builder.io/sdk-svelte';

  // Add your Public API Key
  const BUILDER_PUBLIC_API_KEY = "af78a16b5e3245c0aa1e501ea73f4c6c"; 

  let content = undefined;
  let canShowContent = false;

  const fetch = async () => {
    // fetch your Builder content
    content = await getContent({
      model: 'page',
      apiKey: BUILDER_PUBLIC_API_KEY,
      userAttributes: {
        urlPath: window.location.pathname || '/'
      }
    });

    // handle preview mode
    canShowContent = Boolean(content || isPreviewing());
  };

  fetch();
</script>

<main>
  <h1>
    Welcome to your Builder-integrated Svelte app
  </h1>
  <div>Below is your Builder Content:</div>

  {#if canShowContent}
    <!-- Render builder content with all required props -->
    <RenderContent
      model="page"
      {content}
      apiKey={BUILDER_PUBLIC_API_KEY}
    />
  {:else}
    Content Not Found
  {/if}
</main>
