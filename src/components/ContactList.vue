<template>
  <div class="contact-list">
    <h2>Contactos</h2>
    <table>
      <thead>
        <tr>
          <th>Nombre</th>
          <th>Correo</th>
          <th>Teléfono</th>
          <th>País</th>
          <th>Ciudad</th>
          <th>Acciones</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="contact in filteredContacts" :key="contact.id">
          <td>{{ contact.name }}</td>
          <td>{{ contact.email }}</td>
          <td>{{ contact.phone }}</td>
          <td>{{ contact.country }}</td>
          <td>{{ contact.city }}</td>
          <td>
            <button @click="$emit('edit', contact)">Editar</button>
            <button @click="$emit('delete', contact.id)">Eliminar</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  props: ['contacts', 'filteredContacts'],
};
</script>