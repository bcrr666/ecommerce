<template>
  <div class="p-4">
    <div class="h3">Lista de Cursos</div>
    <div class="row mt-4">
        <div v-for="(item, index) in courses" :key="index" class="col-md-4 mt-4">
          <div style="width: 200px; border: 1px solid; border-radius: 10px; padding: 10px;" class="p-4 text-center">
            <div class="h2 text center">{{item.name}}</div>
            <div>{{item.resume}}</div>
            <div>
              <img :src="item.img" alt="" style="width:150px;" class="mt-2">
            </div>
            <div class="mt-2 h5">{{item.author}}</div>
          </div>
        </div>
    </div>
  </div>
</template>

<script>

export default {
  middleware: 'guest',
  name: 'MainDashboard',
   data() {
      return {
        courses: [],
      }
  },
  methods: {
    getCourses() {
        this.$axios.get('/api/enrollment/search')
        .then(response => {
          this.courses = response.data.data
        })
        .catch(error => {
            console.log('error', error)
        })
    },
    async logout() {
      await this.$auth.logout();
    },
  },
  created() {
    this.getCourses()
  }
}
</script>
