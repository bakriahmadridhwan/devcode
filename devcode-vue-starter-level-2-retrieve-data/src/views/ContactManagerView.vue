<template>
  <div class="home">
    <div class="container">
      <input-contact-form title="Devcode Contact Manager" />
      <div class="contact-list__container">
        <!-- TODO: Uncomment baris kode di bawah ini untuk menampilkan komponen ContactItem yang berisi data kontak sesuai dengan jumlah data kontak yang didapat dari API -->
        <contact-item
          v-for="contact in contactsData"
          :key="contact.id"
          :id="contact.id"
          :full_name="contact.full_name"
          :phone_number="contact.phone_number"
          :email="contact.email"
        />
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import InputContactForm from "@/components/InputContactForm.vue";

// TODO: Uncomment baris kode di bawah untuk meng-import komponen ContactItem
import ContactItem from "@/components/ContactItem.vue";

export default {
  name: "ContactManagerView",
  components: {
    InputContactForm,

    // TODO: Uncomment barus kode di bawah untuk menambahkan ContactItem sebagai komponen pada file ini
    ContactItem,
  },
  data() {
    return {
      // TODO: Uncomment baris kode di bawah ini untuk membuat variabel baru sebagai wadah dari list data kontak yang akan diambil dari API
      contactsData: [],
    };
  },
  mounted() {
    // TODO: Uncomment baris kode di bawah ini untuk memanggil fungsi getAllContactsData setelah halaman contacts selesai dirender
    this.getAllContactsData();
  },
  methods: {
    // TODO: Uncomment baris kode di bawah ini untuk membuat fungsi getAllContactsData yang akan men-dispatch fungsi mengambil data kontak dari api yang sudah dibuat sebelumnya di store/index.js dan menyimpan data kontak ke dalam variabel contactsData
    async getAllContactsData() {
      const response = await this.$store.dispatch("getAllContactsData");
      this.contactsData = response.data.data;
      console.log(response.data.data);
    },
  },
};
</script>

<style lang="scss" scoped>
.home {
  display: flex;
  justify-content: center;

  .container {
    padding: 18px;
    width: 50%;
    height: 100%;
    border: solid 4px #d4d4d4;
    background: #f4f4f4;

    .contact-list {
      &__container {
        margin-top: 48px;
        display: flex;
        flex-direction: column;
        align-items: center;
      }
    }
  }
}
</style>
