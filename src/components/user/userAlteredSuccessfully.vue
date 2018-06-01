<template>
  <div class="card align-items-center">
    <div class="card-text form-group"> Les détails de l'utilisateur ont été modifiés!</div>
    <div class="col-md-2 col-lg-2 col-xl-2 col-sm-3 col-12 mb-5 form-group">
      <button @click="movetoonepage"
      role="buttton"
      class="btn btn-sm btn-secondary form-control cursor">
      Retourner
      </button>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    movetoonepage () {
      this.$router.go(-1)
    }
  },
  mounted () {
    $('.modal-backdrop').removeClass('modal-backdrop')
  }
}
</script>

<style scoped>
.card {
  padding: 15vh;
}
</style>
