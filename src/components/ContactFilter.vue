<template>
  <div class="contact-filter">
    <h2>Filtrar Contactos</h2>
    <input v-model="filters.name" placeholder="Buscar por nombre" />
    <input v-model="filters.email" placeholder="Buscar por correo" />
    <button @click="applyFilters">Filtrar</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      filters: {
        name: '',
        email: '',
      },
    };
  },
  methods: {
    applyFilters() {
      this.$emit('filter', { ...this.filters }); // Emitimos los filtros de forma correcta
    },
  },
};
</script>