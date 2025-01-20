<template>
  <div id="app">
    <ContactFilter @filter="filterContacts" />
    <ContactList
      :contacts="contacts"
      :filteredContacts="filteredContacts"
      @edit="editContact"
      @delete="deleteContact"
    />
    <ContactForm
      :contact="currentContact"
      :isEditing="isEditing"
      @add="addContact"
      @update="updateContact"
      @reset="resetForm"
    />
  </div>
</template>

<script>
import ContactList from './components/ContactList.vue';
import ContactForm from './components/ContactForm.vue';
import ContactFilter from './components/ContactFilter.vue';

export default {
  components: { ContactList, ContactForm, ContactFilter },
  data() {
    return {
      contacts: [
        {
          id: 1,
          name: 'Alicia Perez Loza',
          email: 'aliceia.perez@gmail.com',
          address: '123 Maple Street',
          phone: '123-456-7890',
          country: 'USA',
          city: 'New York',
        },
        {
          id: 2,
          name: 'Bob Smith',
          email: 'bob.smith@hotmail.com',
          address: '456 Oak Avenue',
          phone: '987-654-3210',
          country: 'Canada',
          city: 'Toronto',
        },
        {
          id: 3,
          name: 'Eliana Sanchez',
          email: 'eliana.sanchez@gmail.com',
          address: 'Calle Nor Lipez #1547 - Zona Sud',
          phone: '74859621',
          country: 'Bolivia',
          city: 'Cochabamba',
        },
        {
          id: 4,
          name: 'Maria Cordoba',
          email: 'maria.cordoba@gmail.com',
          address: 'Calle MAtias Terrazas #254 - Zona Miraflores',
          phone: '67854216',
          country: 'Bolivia',
          city: 'La Paz',
        },
        {
          id: 5,
          name: 'Jose Ximenez',
          email: 'jose.ximenez@gmail.com',
          address: 'Calle los Sargentos # 154hl - Zona Cortez',
          phone: '757-667-32122',
          country: 'Mexico',
          city: 'Juarez',
        },
      ],
      filteredContacts: [],
      currentContact: {
        id: null,
        name: '',
        email: '',
        address: '',
        phone: '',
        country: '',
        city: '',
      },
      isEditing: false,
    };
  },
  created() {
    this.filteredContacts = [...this.contacts];
  },
  methods: {
    addContact(contact) {
      contact.id = Date.now();
      this.contacts.push(contact);
      this.filterContacts({ name: '', email: '' });  // Actualizamos los contactos filtrados
    },
    editContact(contact) {
      this.currentContact = { ...contact };
      this.isEditing = true;
    },
    updateContact(contact) {
      const index = this.contacts.findIndex((c) => c.id === contact.id);
      if (index !== -1) {
        this.contacts[index] = { ...contact };
      }
      this.filterContacts({ name: '', email: '' });  // Actualizamos los contactos filtrados
      this.resetForm();
    },
    deleteContact(id) {
      this.contacts = this.contacts.filter((c) => c.id !== id);
      this.filterContacts({ name: '', email: '' });  // Actualizamos los contactos filtrados
    },
    filterContacts(filters) {
      this.filteredContacts = this.contacts.filter(
        (c) =>
          c.name.toLowerCase().includes(filters.name.toLowerCase()) &&
          c.email.toLowerCase().includes(filters.email.toLowerCase())
      );
    },
    resetForm() {
      this.currentContact = {
        id: null,
        name: '',
        email: '',
        address: '',
        phone: '',
        country: '',
        city: '',
      };
      this.isEditing = false;
    },
  },
};
</script>
