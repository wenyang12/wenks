<template>
  <div class="list">
   <!-- 添加图片按钮 -->
    <mu-float-button icon="add" class="add-movie-button" backgroundColor @click="openAddPicModal"/>
    <!-- 添加图片表单 -->
    <vodal :show="addMovieModal" animation="slideDown" :width="500" :height="480" :closeButton="false">
      <mu-text-field v-model="title" fullWidth icon="movie" label="图片名称" labelFloat/><br/>
      <mu-text-field v-model="url" fullWidth icon="picture_in_picture" label="图片地址" labelFloat/><br/>
      <mu-raised-button @click="addPic" label="确定" icon="check" primary/>
    </vodal>
  </div>
</template>

<script>
export default {
  name: 'Add',
  created () {
    document.title = this.$route.name
  },

  data () {
    return {
      title: '',
      url: '',
      addMovieModal: false
    }
  },
  methods: {
    // 访问后端添加电影的方法
    openAddPicModal () {
      this.addMovieModal = true
    },
    addPic () {
      this.$http.post('/api/add', {
        title: this.title,
        url: this.url
      })
      .then(res => {
        this.toastr.success('添加成功')
        this.title = ''
        this.url = ''
      })
      .catch(e => {
        this.toastr.warn('保存失败!')
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
