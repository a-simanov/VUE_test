<template>
  <div>
    <div class="container column">
    <app-form></app-form>

    <div class="card card-w70">
      <h1>Резюме Nickname</h1>
      <div class="avatar">
        <img src="https://cdn.dribbble.com/users/5592443/screenshots/14279501/drbl_pop_r_m_rick_4x.png">
      </div>
      <h2>Опыт работы</h2>
      <p>
        главный герой американского мультсериала «Рик и Морти», гениальный учёный, изобретатель, атеист (хотя в некоторых сериях он даже молится Богу, однако, каждый раз после чудесного спасения ссылается на удачу и вновь отвергает его существование), алкоголик, социопат, дедушка Морти. На момент начала третьего сезона ему 70 лет[1]. Рик боится пиратов, а его главной слабостью является некий - "Санчезиум". Исходя из того, что существует неограниченное количество вселенных, существует неограниченное количество Риков, герой сериала предположительно принадлежит к измерению С-137. В серии комикcов Рик относится к измерению C-132, а в игре «Pocket Mortys» — к измерению C-123[2]. Прототипом Рика Санчеза является Эмметт Браун, герой кинотрилогии «Назад в будущее»[3].
      </p>
      <h3>Добавьте первый блок, чтобы увидеть результат</h3>
    </div>
  </div>
    <div class="container">
      <app-loader v-if="loader"></app-loader>
      <app-comments v-else :comments="comments" @load-comments="loadComments"></app-comments>
    </div>
  </div>
</template>

<script>
import AppForm from './components/AppForm.vue'
import AppLoader from './components/AppLoader.vue'
import AppComments from './components/AppComments'

export default {
  data () {
    return {
      loading: false,
      comments: []
    }
  },
  methods: {
    async loadComments() {
      this.loading = true
      const res = await fetch('https://jsonplaceholder.typicode.com/comments?_limit=42')
      this.comments = await res.json()
      console.log(this.comments)
      this.loading = false
    },
  },
  components: {AppForm, AppLoader, AppComments}
}
</script>

<style>
  .avatar {
    display: flex;
    justify-content: center;
  }

  .avatar img {
    width: 150px;
    height: auto;
    border-radius: 50%;
  }
</style>
