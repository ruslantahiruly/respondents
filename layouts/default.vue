<template>
  <div id="page">
    <div id="sidebar">
      <TheNavbar />
    </div>
    <div id="main">
      <TheHeader />
      <main>
        <Nuxt />
      </main>
    </div>
  </div>
</template>

<style lang="scss" scoped>
#page {
  display: flex;
}

#main {
  margin-bottom: 5rem;
}

// main {
//   margin-bottom: 10rem;
// }

#sidebar {
  padding-bottom: 5rem;
}
</style>
