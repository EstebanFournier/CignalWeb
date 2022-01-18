<template>
  <div>
  <TheHeader />
    <h1>Dashboard</h1>
    <NuxtLink :to="`/certificats/`">
      <h2>Certificats</h2>
    </NuxtLink>
    <br>
    <NuxtLink :to="`/alerts/`">
      <h2>Alertes</h2>
    </NuxtLink>
    <br>
    <NuxtLink :to="`/emails`">
      <h2>Emails</h2>
    </NuxtLink>
  </div>
</template>

<script>
export default {};
</script>
