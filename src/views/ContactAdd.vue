<template>
    <div v-if="contact" class="page">
        <h4>Thêm mới liên hệ</h4>
        <ContactForm :contact="contact" @submit:contact="uploadContact" />
        <p>{{ message }}</p>
    </div>
</template>
<script>
import ContactForm from "@/components/ContactForm.vue";
import ContactService from "@/services/contact.service";
export default {
    components: {
        ContactForm,
    },
    props: {
        id: { type: String, required: true },
    },
    data() {
        return {
            contact: {},
            message: "",
        };
    },
    methods: {
        async uploadContact(data) {
            try {

                await ContactService.create(data) 
                this.message = "Thêm mới liên hệ thành công";
            } catch (error) {
                console.log(error);
            }
        }
    }
}
</script>