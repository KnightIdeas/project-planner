<template>
  <form @submit.prevent="handleSubmit">
    <label>Title:</label>
    <input type="text" v-model="title" required>
    <label>Details:</label>
    <textarea v-model="details" required></textarea>
    <button>Update Project</button>
  </form>
</template>

<script>
export default {
    props: ['id'],
    data() {
        return {
            title: '',
            details: '',
            uri: 'https://api.jsonbin.io/v3/b/67d048b28960c979a56f934d' + this.id
        }
    },
    methods: {
        handleSubmit() {
        let project = {
            title: this.title,
            details: this.details
        }
        fetch(this.uri, {
            method: 'PATCH',
            headers: { 'X-Master-Key': '$2a$10$gdgb7AztntbJrBTaxbitR.rM20kLV/LN2k8Ur9rpaV.U7vNBK5ryq' },
            body: JSON.stringify(project)
        }).then(() => {this.$router.push('/')

        }).catch((err) => console.log(err))
    },
},
    mounted() {
        fetch(this.uri)
        .then(res => res.json())
        .then(data => {
            this.title = data.title
            this.details = data.details
        })
    }

}
</script>

<style>

</style>