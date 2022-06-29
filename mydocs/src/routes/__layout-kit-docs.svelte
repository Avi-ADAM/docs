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
  //let baseUrl = 'https://hadracha.1lev1.world/';
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
    links: [
       { title: 'הרשמה', slug: 'https://www.1lev1.world/' },
      { title: 'מסלולים', slug: 'https://shalom.1lev1.world/' },
      { title: 'המדריך', slug: '/docs', match: /\/docs/ },
  ],
  };

  /** @type {import('@svelteness/kit-docs').SidebarConfig} */
</script>

<svelte:head>
  
      <title>המדריך 1❤️1</title>
   
      <meta name="description" content="הדרכה לשימוש באתר 1❤️1" />
   
</svelte:head>
<KitDocs {meta}>
  <KitDocsLayout {navbar} {i18n}>
    <div class="logo" slot="navbar-left">
      <Button href="/">

       {@html `<img src="${baseUrl}favicon.png" alt="logo" height="60px" width="60px"/>`}
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
