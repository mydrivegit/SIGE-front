<template>
  <div class="card cardInEmailSP">
    <div class="card-text"> Votre message a été envoyé avec succès! </div>
    <a @click="movetoonepage"
    role="buttton"
    class="btn btn-sm btn-secondary cursor">
    Retourner
    </a>
  </div>

</template>

<script>
export default {
  methods: {
    movetoonepage () {
      this.$router.go(-1)
    }
  }
}
</script>

<style>
.cardInEmailSP {
  padding: 15vh;
}
</style>
