<template>
<div class="container register">
  <div class="row justify-content-md-center">
    <div class="card-wrapper col-md-5 col-sm-9 col-lg-5 col-xl-5">
      <div class="card fat">
        <div class="card-body">
          <h4 class="card-title text-center">
              Inscrire d'utilisateur
          </h4>
          <form @submit.prevent="register">
            <div class="form-group">
              <label for="username" class="sr-only">Identification </label>
              <input class="form-control form-control-sm" v-model="user.username" placeholder="Identification" type="text" autofocus required>
            </div>
            <div class="form-group">
              <label for="lastname" class="sr-only">Nom de famille</label>
              <input class="form-control form-control-sm" v-model="user.lastname" placeholder="Nom de famille" type="text" required>
            </div>
            <div class="form-group">
              <label for="firstname" class="sr-only">Prénom</label>
              <input class="form-control form-control-sm" v-model="user.firstname" placeholder="Prénom" type="text" required>
            </div>
            <div class="form-group">
              <label for="email" class="sr-only">E-Mail Adresse</label>
              <input class="form-control form-control-sm" v-model="user.email" placeholder="E-Mail Adresse" type="email" required>
            </div>
            <div class="form-group">
              <label for="role" class="sr-only">Rôle</label>
              <select  v-model="user.role"  class="form-control form-control-sm" required>
                  <option disabled value='null'>Sélectionnez le rôle......</option>
                  <option value='Admin'>Administrateur</option>
                  <option value='User'>Utilisateur</option>
              </select>
            </div>
            <div class="form-group">
              <label for="mobileNo" class="sr-only">Numéro de portable</label>
              <input class="form-control form-control-sm" v-model="user.mobileNo" placeholder="Numéro de portable" type="number" required>
            </div>
            <div class="form-group">
              <label for="password" class="sr-only">Mot de passe</label>
              <input class="form-control form-control-sm" type="password" v-model="user.password" placeholder="Mot de passe" required>
            </div>
            <div class="form-group no-margin">
                <button class="btn btn-secondary btn-block">S'inscrire</button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</div>
</template>

<script>
export default {
  data () {
    return {
      user: {
        firstname: '',
        lastname: '',
        email: '',
        mobileNo: '',
        role: null,
        username: '',
        password: ''
      }
    }
  },
  methods: {
    register () {
      this.$store.dispatch('register', this.user)
        .then(res => {
          if (res.status === 201) {
            this.$router.push({name: 'listOfUser'})
            this.$swal('Account ' + this.user.username + ' created Succesfully : please login')
          }
        })
        .catch(err => {
          console.log(err)
          this.$swal('Username already exist')
        })
    }
  },
  computed: {
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.register {
    padding-top: 10vh;
    padding-left: 5vh;
}

</style>
