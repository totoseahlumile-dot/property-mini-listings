<template>
  <div class="property-card" :class="{ unavailable: !property.available }">
    <div class="card-image-wrap">
      <img class="card-image" :src="property.image" :alt="property.title" />

      <div class="card-tags">
        <span class="tag light">{{ property.location }}</span>
        <span class="tag">{{ property.type }}</span>
      </div>

      <span v-if="!property.available" class="unavailable-ribbon">Not Available</span>

      <button
        class="bookmark-btn"
        :title="isBookmarked ? 'Remove from saved' : 'Save this stay'"
        @click="$emit('toggle-bookmark', property.id)"
      >
        {{ isBookmarked ? '❤' : '🤍' }}
      </button>
    </div>

    <div class="card-body">
      <div class="card-location">
        <span> {{ property.location }}, Western Cape</span>
        <span class="rating">★ {{ property.rating }} ({{ property.reviews }})</span>
      </div>

      <h3 class="card-title">{{ property.title }}</h3>
      <p class="card-description">{{ property.description }}</p>

      <div class="card-meta">
        <div class="meta-item">
          <strong>{{ property.bedrooms }}</strong>
          Bedrooms
        </div>
        <div class="meta-item">
          <strong>{{ property.bathrooms }}</strong>
          Bathrooms
        </div>
        <div class="meta-item">
          <strong>{{ property.guests }}</strong>
          Guests
        </div>
      </div>

      <div class="card-footer">
        <div>
          <span class="price-currency">ZAR</span>
          <span class="price-value"> R {{ property.price.toLocaleString() }}</span>
          <span class="price-period">per night</span>
        </div>

        <button class="enquire-btn" :disabled="!property.available">
          {{ property.available ? 'Enquire Now' : 'Unavailable' }}
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'PropertyCard',
  props: {
    // the property object holds all the listing details
    property: {
      type: Object,
      required: true
    },
    // whether this card has been saved/favourited by the user
    isBookmarked: {
      type: Boolean,
      default: false
    }
  },
  emits: ['toggle-bookmark']
}
</script>
