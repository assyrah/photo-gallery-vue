<template>
  <div class="layout">
    <header class="header">
      <div class="header header-nav container">
        <span class="logo navbar-item"></span>
      </div>
    </header>
    <slot/>
    <footer class="footer">
    </footer>
  </div>
</template>

<static-query>
query {
  metadata {
    siteName
  }
}
</static-query>

<style lang="scss">
  @import "~/assets/scss/main.scss"
</style>
