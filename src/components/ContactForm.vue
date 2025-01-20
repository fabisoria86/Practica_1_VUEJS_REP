<template>
  <div class="contact-form">
    <h2>{{ isEditing ? "Editar Contacto" : "Agregar Contacto" }}</h2>
    <form @submit.prevent="handleSubmit">
      <div>
        <label>Nombre:</label>&nbsp;&nbsp;
        <input v-model="form.name" required />
      </div>
      <br />
      <div>
        <label>Correo:</label>&nbsp;&nbsp;&nbsp;&nbsp;
        <input v-model="form.email" type="email" required />
      </div>
      <br />
      <div>
        <label>Dirección:</label>&nbsp;
        <input v-model="form.address" />
      </div>
      <br />
      <div>
        <label>Teléfono:</label>&nbsp;&nbsp;
        <input v-model="form.phone" />
      </div>
      <br />
      <div>
        <label>País:</label>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
        <input v-model="form.country" />
      </div>
      <br />
      <div>
        <label>Ciudad:</label>&nbsp;&nbsp;
        <input v-model="form.city" />
      </div>
      <br />
      <button type="submit">{{ isEditing ? "Actualizar" : "Agregar" }}</button>
      <button type="button" @click="resetForm">Cancelar</button>
    </form>
  </div>
</template>

<script>
export default {
  props: ['contact', 'isEditing'],
  data() {
    return {
      form: { ...this.contact },  // Inicializamos el formulario con los datos del contacto actual
    };
  },
  watch: {
    // Actualizamos el formulario cuando cambian los props
    contact(newVal) {
      this.form = { ...newVal };
    }
  },
  methods: {
    handleSubmit() {
      this.$emit(this.isEditing ? 'update' : 'add', this.form);
      this.resetForm();
    },
    resetForm() {
      this.$emit('reset');
    },
  },
};
</script>