<template>
  <header class="app-header">
    <div class="container header-inner">
      <div class="brand">
        <div class="brand-icon"></div>
        <div class="brand-text">
          <h1>
            Homes &amp; Beyond
            <span class="city-tag">CAPE TOWN</span>
          </h1>
          <p> Short-Term Rentals &amp; Coastal Stays</p>
        </div>
      </div>

      <div class="header-stats">
        <span class="stat-pill">Total: {{ totalCount }}</span>
        <span class="stat-pill active">Active: {{ activeCount }}</span>
        <span class="stat-pill">❤ Saved: {{ savedCount }}</span>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  name: 'AppHeader',
  props: {
    
    totalCount: {
      type: Number,
      required: true
    },
    
    activeCount: {
      type: Number,
      required: true
    },
    
    savedCount: {
      type: Number,
      default: 0
    }
  }
}
</script>
