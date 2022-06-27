<!-- This layout inherits from `routes/__layout-kit-docs.svelte` -->
<!-- Learn more: https://kit.svelte.dev/docs/layouts#named-layouts-inheritance-chains -->

<script context="module">
  export const prerender = true;

  export const load = createKitDocsLoader({
    sidebar: {
      '/': null,
      '/docs': '/docs',
    },
  });
</script>

<script>
  import '@svelteness/kit-docs/client/polyfills/index.js';
  import '@svelteness/kit-docs/client/styles/normalize.css';
  import '@svelteness/kit-docs/client/styles/fonts.css';
  import '@svelteness/kit-docs/client/styles/vars.css';
  import '@svelteness/kit-docs/client/styles/theme.css';
  import './../main.css';
  import { page } from '$app/stores';
  let baseUrl = 'http://localhost:2000/';
  import {
    Button,
    KitDocs,
    KitDocsLayout,
    createKitDocsLoader,
    createSidebarContext,
  } from '@svelteness/kit-docs';

    const i18n = {
  nav: {
    previous: 'הקודם',
    next: 'הבא',
    mainMenu: 'תפריט צד ראשי',
    openSidebar: 'פתיחת תפריט צד ראשי',
    options: 'אפשרויות',
    links: 'לינקים',
  },
   colorScheme: {
    title: 'בחירת ערכת נושא',
    light: 'מואר',
    dark: 'חשוך',
    system: 'ברירת מחדל',
    theme: 'ערכת נושא',
  },
  toc: {
    title: 'בדף הזה',
  },
  dialog: {
    close: 'סגירת הדיאלוג',
  },
  admonition: {
    note: 'הערה',
    info: 'מידע',
    tip: 'טיפ',
    warning: 'אזהרה',
    danger: 'סכנה',
    experimental: 'נסיוני',
  },
  code: {
    copy: 'העתקת קוד',
    copied: 'הקוד הועתק',
  },
  }
  /** @type {import('@svelteness/kit-docs').MarkdownMeta | null} */
  export let meta;

 
  /** @type {import('@svelteness/kit-docs').NavbarConfig} */
  const navbar = {
    links: [{ title: 'המדריך', slug: '/docs', match: /\/docs/ }],
  };
  import ExperimentalIcon from '~icons/ri/test-tube-fill';

  /** @type {import('@svelteness/kit-docs').SidebarConfig} */
  export let sidebar;


  const { activeCategory } = createSidebarContext(sidebar);

  $: category = $activeCategory ? `${$activeCategory}: ` : '';
  $: title = meta ? `${category}${meta.title} | KitDocs` : null;
  $: description = meta?.description;
</script>

<svelte:head>
  {#key $page.url.pathname}
    {#if title}
      <title>{title}</title>
    {/if}
    {#if description}
      <meta name="description" content={description} />
    {/if}
  {/key}
</svelte:head>
<KitDocs {meta}>
  <KitDocsLayout {navbar} {sidebar} {i18n}>
    <div class="logo" slot="navbar-left">
      <Button href="/">

       {@html `<img src="http://localhost:2000/favicon.png" alt="logo" height="60px" width="60px"/>`}
      </Button>
    </div>
 
    <slot />
  </KitDocsLayout>
</KitDocs>
<style>
 
  :global(:root) {
    --kd-color-brand-rgb: 255, 0, 146; /*233,127,6*/
  }

  :global(:root.dark) {
    --kd-color-brand-rgb: 238, 232, 170; /*213, 149, 76;*/
  }

  .logo :global(a) {
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .logo :global(svg) {
    height: 36px;
    overflow: hidden;
  }
</style>
