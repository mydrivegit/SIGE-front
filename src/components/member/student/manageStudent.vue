<template>
<div>
  <div class="container ins-container col-10">
      <h4 class="text-nowrap text-center w-100 mb-5 form-control-sm heading">
        <strong class="text-uppercase markdown-body">Fiche élève</strong>
      </h4>
        <form @submit.prevent="modify">
          <div class="form-row align-self-center">
            <div class="col-md-4">
              <label class="col-form-label font-weight-bold">Statut</label>
              <select v-model="student.status"  class="form-control is-valid"
              data-toggle="tooltip" data-placement="bottom" title="Statut" required>
              <option disabled value='null'>Sélectionnez le status......</option>
              <option value='true'>Actif</option>
              <option value='false'>Inactif</option>
            </select>
            </div>
            <div class="col-md-4">
              <label class="col-form-label  font-weight-bold">Classe</label>
              <select v-model="student.class"  class="form-control is-valid"
              data-toggle="tooltip" data-placement="bottom" title="Classe" required>
              <option disabled value='null'>Sélectionnez la classe......</option>
              <option v-for="item in classes" :key="item._id" v-show="item.status">{{item.name}} {{item.code}} </option>
            </select>
            </div>
            <div class="col-md-4" >
              <label class="col-form-label  font-weight-bold">Responsable</label>
            <select v-model="student.inCharge"  class="form-control is-valid"
              data-toggle="tooltip" data-placement="bottom" title="Statut">
              <option disabled value='null'>Sélectionnez le responsable......</option>
              <option v-for="item in members" :key="item._id" v-show="item.roleInCharge">{{item.lastname}} {{item.firstname}} </option>
            </select>
            </div>
          </div>
          <div class="form-row">
            <div class="col-md-4">
              <label class="col-form-label  font-weight-bold">Nom</label>
              <input v-model="student.lastname" type="text" class="form-control is-valid" data-toggle="tooltip" data-placement="bottom" title="Nom" required>
            </div>
            <div class="col-md-4">
              <label class="col-form-label  font-weight-bold">Prénom</label>
              <input v-model="student.firstname" type="text" class="form-control is-valid" data-toggle="tooltip" data-placement="bottom" title="Prénom"  required>
            </div>
            <div class="col-md-4">
              <label class="col-form-label  font-weight-bold">Date de naissance</label>
              <input v-model="student.dob" placeholder="JJ/MM/YYYY" class="form-control date is-valid" data-toggle="tooltip" data-placement="bottom" title="Date de naissance">
            </div>
          </div>
          <div class="form-row">
            <div class="col-md-4">
              <label class="col-form-label  font-weight-bold">Genre</label>
              <select v-model="student.gender" class="form-control is-valid"
              data-toggle="tooltip" data-placement="bottom" title="Genre" required>
                  <option disabled value='null'>Sélectionnez le genre......</option>
                  <option>Homme</option>
                  <option>Femme</option>
                </select>
            </div>
            <div class="col-md-4">
              <label class="col-form-label  font-weight-bold">Mobile</label>
              <input v-model="student.mobileNo" type="tel" class="form-control is-valid" data-toggle="tooltip" data-placement="bottom" title="Mobile"  required>
            </div>
            <div class="col-md-4">
              <label class="col-form-label  font-weight-bold">Téléphone</label>
              <input v-model="student.telephone" type="tel" class="form-control is-valid" data-toggle="tooltip" data-placement="bottom" title="Télèphone"  required>
            </div>
          </div>
          <div class="form-row">
            <div class="col-md-12">
              <label class="col-form-label  font-weight-bold">Email</label>
              <input v-model="student.email" type="email" class="form-control is-valid" data-toggle="tooltip" data-placement="bottom" title="l'Adresse Email" required>
            </div>
          </div>
          <div class="form-row mb-4">
            <div class="col-md-4">
              <label class="col-form-label  font-weight-bold">Adresse</label>
              <input v-model="student.address" type="text" class="form-control is-valid" data-toggle="tooltip" data-placement="bottom" title="Adresse" required>
            </div>
            <div class="col-md-4">
              <label class="col-form-label  font-weight-bold">Code postal</label>
              <input v-model="student.cp" type="number" pattern="[0-9]{5}" class="form-control is-valid" data-toggle="tooltip" data-placement="bottom" title="code postale" required>
            </div>
            <div class="col-md-4">
              <label class="col-form-label  font-weight-bold">Ville</label>
              <input v-model="student.town" type="text" class="form-control is-valid" data-toggle="tooltip" data-placement="bottom" title="Ville" required>
            </div>
          </div>
          <button class="btn btn-secondary  mb-5">Enregistrer</button>
        </form>
        </div>
        <div class="container ins-container table-responsive col-10 mb-4">
        <table class="col table table-striped table-hover mb-0">
          <thead class="thead-light">
            <tr class="text-left col">
              <th style="width: 20vh" scope="col" >Absence <!-- <i class="fa fa-sort-asc"></i> --></th>
              <th style="width: 20vh" scope="col">Date <!-- <i class="fa fa-sort"></i> --></th>
              <th style="width: 20vh" scope="col">Matière <!-- <i class="fa fa-sort"></i> --></th>
              <!-- <th style="width: 20vh" scope="col">Notification <i class="fa fa-sort"></i></th> -->
              <!--style="width: 30%"  <th scope="col">Date de Notification <i class="fa fa-sort-desc"></i></th> -->
              <th style="width: 40vh" scope="col">Commentaire </th>
            </tr>
          </thead>
          <tbody v-for="details in attMemberId" :key="details._id">
            <tr @click="viewAttendence(details._id)" class="cursor content">
              <th>{{details.classId.label}}</th>
              <th>{{moment(details.dateOfAttendence).format('L')}}</th>
              <td>{{details.subjectId.name}}</td>
              <!-- <td>En attente</td> -->
              <!-- <td>12/12/2018 à 09h30</td> -->
              <td>{{details.comment}}</td>
            </tr>
          </tbody>
        </table>
        <a>
          <button @click="addAttendence()"  class="btn btn-secondary mb-2">
            <i class="fa fa-calendar-plus-o"></i> Ajouter un Absent(e)</button>
        </a>
        </div>
        <div class="container table-responsive ins-container col-10">
        <table class="col table  table-striped table-hover">
          <thead class="thead-light">
            <tr class="text-left">
              <th scope="col">Classe  <!-- <i class="fa fa-sort-asc"></i> --></th>
              <th scope="col">Code <!-- <i class="fa fa-sort"></i> --></th>
              <th scope="col">Année Scolaire <!-- <i class="fa fa-sort"></i> --></th>
              <th scope="col">Statut <!-- <i class="fa fa-sort-desc"></i> --></th>
            </tr>
          </thead>
          <tbody v-for="classDetails in memberInClass" :key="classDetails._id">
            <tr class="content">
              <th>{{classDetails.label}}</th>
              <th>{{classDetails.code}}</th>
              <th>{{classDetails.year}}</th>
              <td><div v-if="classDetails.status">Active</div>
              <div v-else>Inactive</div></td>
            </tr>
          </tbody>
        </table>
        </div>
</div>
</template>

<script>
import { mapGetters, mapActions } from 'vuex'
export default {
  data () {
    return {
      show: true
    }
  },
  methods: {
    modify () {
      this.$store.dispatch('modifyMemberIdData', {data: this.student, id: this.$route.params.memberId})
        .then(res => {
          if (res.status === 201) {
            this.$router.push({name: 'listOfMembers'})
            this.$swal('Élève ' + this.student.lastname + ' est modifée avec succès')
          }
        })
        .catch(err => {
          console.log(err)
          this.$swal('Erreur lors de la sauvegarde des détails de ' + this.student.lastname)
        })
    },
    addAttendence () {
      this.$router.push({ name: 'attendence', params: { memberId: this.$route.params.memberId } })
    },
    viewAttendence (arg) {
      this.$router.push({ name: 'manageAttendence', params: { memberId: this.$route.params.memberId, attendenceId: arg } })
    }
  },
  computed: {
    ...mapGetters({
      student: 'memberId',
      members: 'members',
      memberInClass: 'memberInClass',
      attMemberId: 'attMemberId',
      classes: 'classes'
    }),
    ...mapActions([('fetchMembersList')])
  },
  created () {
    this.$store.dispatch('fetchMemberId', this.$route.params.memberId)
    this.$store.dispatch('fetchClassDetailsOfMember', this.$route.params.memberId)
    this.$store.dispatch('fetchAttMemberId', this.$route.params.memberId)
    this.$store.dispatch('fetchClassesList')
    return this.fetchMembersList
  }
}
</script>

<style scoped>
</style>
