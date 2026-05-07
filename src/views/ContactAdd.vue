<template>
    <div class="page">
        <h4>Tạo liên hệ</h4>
        <ContactForm :contact="contact" @submit:contact="uploadContact" />
        <p>{{ message }}</p>
    </div>
</template>
<script>
import ContactForm from '../components/ContactForm.vue';
import ContactService from '../services/contact.service';

export default {
    components: {
        ContactForm
    },
    data() {
        return {
            contact: {},
            message: ""
        }
    },
    methods: {
        async uploadContact(data) {
            try {

                // console.log(data.file);
                await ContactService.create(data)
                this.message = "Liên hệ được tạo thành công.";
                this.$router.push({ name: "contactbook" });
            }
            catch (error) {
                //console.log(error)
                if (error.response?.status === 401) {
    alert("Bạn cần đăng nhập");
    window.location.href = "http://localhost:3000/auth/google";
  }
            }
        }
    },


}
</script>
<style></style>