<template>
  <nav
    :class="[`navbar-${theme}`, `bg-${theme}`, 'navbar', 'navbar-expand-lg']"
  >
    <div class="container-fluid">
      <a
        class="navbar-brand"
        href="#"
        >My Vue</a
      >
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarNavAltMarkup"
        aria-controls="navbarNavAltMarkup"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div
        class="collapse navbar-collapse"
        id="navbarNavAltMarkup"
      >
        <ul class="navbar-nav me-auto">

          <navbar-link
            v-for="(page, index) in publishedPages"
            class="nav-item"
            :key="index"
            :page="page"
            :index="index"
            :isActive="activePage === index"
            @actived="$emit('actived')"
          >
          </navbar-link>

        </ul>
        <form class="d-flex">
          <button
            class="btn btn-primary"
            @click.prevent="changeTheme()"
          >
            Toggle
          </button>
        </form>
      </div>
    </div>
  </nav>
</template>

<script>
  import NavbarLink from './NavbarLink.vue';
  export default {
    components: {
      NavbarLink,
    },
    created() {
      this.getThemeSetting();
    },
    computed: {
      publishedPages() {
        return this.pages.filter((p) => p.published);
      },
    },
    props: ['pages', 'activePage', 'navLinkClick'],
    data() {
      return {
        theme: 'light',
      };
    },
    methods: {
      changeTheme() {
        let theme = 'light';
        if (this.theme == 'light') {
          theme = 'dark';
        }

        this.theme = theme;
        this.storeThemeSetting();
      },
      storeThemeSetting() {
        localStorage.setItem('theme', this.theme);
      },
      getThemeSetting() {
        let theme = localStorage.getItem('theme');

        if (theme) {
          this.theme = theme;
        }
      },
    },
  };
</script>
