<template>
  <div class="list">
    <h1>{{ msg }}</h1>
    <ul>
      <li v-for="pic of pics">{{pic.title}}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'list',
  created () {
    this.getPics()
    document.title = this.$route.name
  },
  data () {
    return {
      msg: '这个是我的相册',
      pics: []
    }
  },
  methods: {
    getPics () {
      this.$http.get('/api/picList')
      .then(res => {
        console.dir(res.data)
        this.pics = res.data
      })
      .catch(err => {
        this.toast.error(`${err.message}`, 'ERROR!')
        console.log(err)
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
