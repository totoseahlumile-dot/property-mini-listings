<template>
  <div>
    <AppHeader
      :total-count="properties.length"
      :active-count="activeCount"
      :saved-count="bookmarkedIds.length"
    />

    <main class="container">
      <FilterBar
        :search-term="searchTerm"
        :sort-order="sortOrder"
        @update:searchTerm="searchTerm = $event"
        @toggle-sort="toggleSort"
      />

      <div v-if="filteredAndSortedProperties.length" class="listings-grid">
        <PropertyCard
          v-for="property in filteredAndSortedProperties"
          :key="property.id"
          :property="property"
          :is-bookmarked="bookmarkedIds.includes(property.id)"
          @toggle-bookmark="toggleBookmark"
        />
      </div>

      <p v-else class="no-results">No properties match your search. Try a different keyword.</p>
    </main>
  </div>
</template>

<script>
import AppHeader from './components/AppHeader.vue'
import FilterBar from './components/FilterBar.vue'
import PropertyCard from './components/PropertyCard.vue'

export default {
  name: 'App',
  components: {
    AppHeader,
    FilterBar,
    PropertyCard
  },
  data() {
    return {
      searchTerm: '',
      sortOrder: 'asc', 
      bookmarkedIds: [],
      
      properties: [
        {
          id: 1,
          title: 'Sea Point Promenade Sunset Apartment',
          location: 'Sea Point',
          type: 'Apartment',
          price: 3400,
          bedrooms: 2,
          bathrooms: 1.5,
          guests: 4,
          rating: 4.85,
          reviews: 88,
          available: true,
          description:
            'Light-filled modern apartment located just 50 meters from the famous Sea Point Promenade and Pavilion swimming pools.',
          image: 'https://images.unsplash.com/photo-1502672260266-1c1ef2d93688?auto=format&fit=crop&w=800&q=80'
        },
        {
          id: 2,
          title: 'Green Point Urban Eco Studio',
          location: 'Green Point',
          type: 'Studio',
          price: 1850,
          bedrooms: 1,
          bathrooms: 1,
          guests: 2,
          rating: 4.79,
          reviews: 114,
          available: true,
          description:
            'Cleverly designed architectural studio overlooking Green Point Urban Park and Cape Town Stadium.',
          image: 'https://images.unsplash.com/photo-1493809842364-78817add7ffb?auto=format&fit=crop&w=800&q=80'
        },
        {
          id: 3,
          title: 'Kirstenbosch Mountain Edge Cottage',
          location: 'Newlands',
          type: 'Cottage',
          price: 2600,
          bedrooms: 2,
          bathrooms: 2,
          guests: 4,
          rating: 4.93,
          reviews: 38,
          available: true,
          description:
            'Peaceful garden sanctuary nestled right against the eastern slopes of Table Mountain, minutes from Kirstenbosch.',
          image: 'https://images.unsplash.com/photo-1568605114967-8130f3a36994?auto=format&fit=crop&w=800&q=80'
        },
        {
          id: 4,
          title: 'Camps Bay Beachfront Loft',
          location: 'Camps Bay',
          type: 'Loft',
          price: 5200,
          bedrooms: 3,
          bathrooms: 2,
          guests: 6,
          rating: 4.9,
          reviews: 61,
          available: false,
          description:
            'Spacious loft with uninterrupted ocean views, steps away from the white sands of Camps Bay beach.',
          image: 'https://images.unsplash.com/photo-1505691938895-1758d7feb511?auto=format&fit=crop&w=800&q=80'
        },
        {
          id: 5,
          title: 'Woodstock Industrial Chic Flat',
          location: 'Woodstock',
          type: 'Flat',
          price: 1450,
          bedrooms: 1,
          bathrooms: 1,
          guests: 2,
          rating: 4.6,
          reviews: 47,
          available: true,
          description:
            'Trendy exposed-brick flat in the heart of Woodstock, close to art galleries, markets and coffee roasters.',
          image: 'https://images.unsplash.com/photo-1484154218962-a197022b5858?auto=format&fit=crop&w=800&q=80'
        },
        {
          id: 6,
          title: 'Constantia Vineyard Guest House',
          location: 'Constantia',
          type: 'Guest House',
          price: 3100,
          bedrooms: 2,
          bathrooms: 2,
          guests: 5,
          rating: 4.88,
          reviews: 52,
          available: false,
          description:
            'Tranquil guest house surrounded by historic vineyards, offering a quiet escape close to the city.',
          image: 'https://images.unsplash.com/photo-1564078516393-cf04bd966897?auto=format&fit=crop&w=800&q=80'
        },
        {
          id: 7,
          title: 'V&A Waterfront Marina Apartment',
          location: 'V&A Waterfront',
          type: 'Apartment',
          price: 4750,
          bedrooms: 2,
          bathrooms: 2,
          guests: 4,
          rating: 4.81,
          reviews: 96,
          available: true,
          description:
            'Elegant apartment overlooking the marina, walking distance from shops, restaurants and the harbour.',
          image: 'https://images.unsplash.com/photo-1512917774080-9991f1c4c750?auto=format&fit=crop&w=800&q=80'
        },
        {
          id: 8,
          title: 'Observatory Backpacker Hideout',
          location: 'Observatory',
          type: 'Room',
          price: 750,
          bedrooms: 1,
          bathrooms: 1,
          guests: 1,
          rating: 4.4,
          reviews: 23,
          available: true,
          description:
            'Budget-friendly room in a lively student neighbourhood, close to UCT and the Lower Main Road cafes.',
          image: 'https://images.unsplash.com/photo-1522708323590-d24dbb6b0267?auto=format&fit=crop&w=800&q=80'
        }
      ]
    }
  },
  computed: {
    
    activeCount() {
      return this.properties.filter((p) => p.available).length
    },
       
    filteredAndSortedProperties() {
      const term = this.searchTerm.trim().toLowerCase()

      let result = this.properties.filter((property) => {
        return (
          property.title.toLowerCase().includes(term) ||
          property.location.toLowerCase().includes(term)
        )
      })

      result = result.slice().sort((a, b) => {
        return this.sortOrder === 'asc' ? a.price - b.price : b.price - a.price
      })

      return result
    }
  },
  methods: {
    toggleSort() {
      this.sortOrder = this.sortOrder === 'asc' ? 'desc' : 'asc'
    },
    toggleBookmark(propertyId) {
      if (this.bookmarkedIds.includes(propertyId)) {
        this.bookmarkedIds = this.bookmarkedIds.filter((id) => id !== propertyId)
      } else {
        this.bookmarkedIds.push(propertyId)
      }
    }
  }
}
</script>
