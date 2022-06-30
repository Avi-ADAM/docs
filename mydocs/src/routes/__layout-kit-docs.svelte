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
      import { variables } from '../tools/variables.js';

  let baseUrl = variables.basePath
 

  import {
    Button,
    KitDocs,
    SocialLink,
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
    links: [
       { title: 'הרשמה', slug: 'https://www.1lev1.world/' },
      { title: 'מסלולים', slug: 'https://shalom.1lev1.world/' },
      { title: 'המדריך', slug: '/docs', match: /\/docs/ },
  ],};

  /** @type {import('@svelteness/kit-docs').SidebarConfig} */
  export const sidebar  =  {
    links: {
      'עלינו': [{
          title: 'עלינו',
          slug: `${baseUrl}docs/עלינו/עלינו`,
      },{
          title: 'ההסכמה',
          slug: `${baseUrl}docs/עלינו/ההסכמה`,
      },{
          title: 'הרשמה',
          slug: `${baseUrl}docs/עלינו/הרשמה`,
      }
    ],
     'להתחיל': [{
          title: 'ליחידים',
          slug: `${baseUrl}docs/להתחיל/ליחידים`,
      },{
          title: 'ריקמה-חדשה',
          slug: `${baseUrl}docs/להתחיל/ריקמה-חדשה`,
      },
    ],
    'רקמות': [{
          title: 'משימות',
          slug: `${baseUrl}docs/רקמות/משימות`,
      },{
          title: 'משאבים',
          slug: `${baseUrl}docs/רקמות/משאבים`,
      },
    ],
    },
  };


  const { activeCategory } = createSidebarContext(sidebar);

  $: category = $activeCategory ? `${$activeCategory}: ` : '';
  $: title = meta ? `${category}${meta.title} | המדריך` : null;
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
<span  dir="rtl">
<KitDocs {meta}>
  <KitDocsLayout {navbar} { sidebar} {i18n}>
    <div  slot="navbar-left">
      <div class="logo">
      <Button href="/">
       {@html `<img src="${baseUrl}favicon.png" alt="logo" height="60px" width="60px"/>`}
      </Button>
    </div>
  </div>
   <div class="socials" slot="navbar-right-alt">
      <SocialLink type="twitter" href="https://twitter.com/l0HTFzdlGHgPhoZ" />
      <SocialLink type="discord" href="https://discord..gg/DNaMwrXzyS" />
    <!--  <SocialLink type="gitHub" href="https://github.com/sveltejs/svelte" />-->
    </div>

    <slot />
  </KitDocsLayout>
</KitDocs>
</span>
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
