<script setup>
import { ref } from 'vue';
// import { useRouter, useRoute } from 'vue-router';
import ContactForm from '@/components/ContactForm.vue';
import contactsService from '@/services/contacts.service';
// const props = defineProps({
//   contactId: { type: String, default: null }
// });
// const router = useRouter();
// const route = useRoute();
const contact = ref({});
const message = ref('');

async function onAddContact(contact) {
  try {
    await contactsService.createContact(contact);
    message.value = 'Liên hệ được thêm thành công.';
  } catch (error) {
    console.log(error);
  }
}
</script>
<template>
  <div v-if="contact" class="page">
    <h4>Thêm Liên hệ</h4>
    <ContactForm :contact="contact" @submit:contact="onAddContact" />
    <p>{{ message }}</p>
  </div>
</template>
