<template>
    
</template>

<script>
    export default {
        props: ['nextUrl'],
        data(){
            return{ name: "", email: "", password: "", password_confirmation: "" }
        },
        methods : {
            handleSubmit(e){
                e.preventDefault()
                if (this.password !== this.password_confirmation || this.password.length <= 0) {
                    this.password = ""
                    this.password_confirmation = ""
                    return alert('Passwords do not match')
                }
                let name = this.name
                let email = this.email
                let password = this.password
                let c_password = this.password_confirmation
                axios.post('api/register', {name, email, password, c_password}).then(response => {
                    let data = response.data
                    localStorage.setItem('bigStore.user', JSON.stringify(data.user))
                    localStorage.setItem('bigStore.jwt', data.token)
                    if (localStorage.getItem('bigStore.jwt') != null){
                        this.$emit('loggedIn')
                        let nextUrl = this.$route.params.nextUrl
                    }
                })
            }
        }
    }
</script>

<style scoped>

</style>