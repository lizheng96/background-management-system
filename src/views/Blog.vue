<template>
  <div id="add-blog">
    <h2>添加博客</h2>
    <form action v-if="!kaiguan">
      <label for>博客标题</label>
      <input type="text" v-model="blog.title" required>
      <label for>写博客</label>
      <textarea name id cols="30" rows="10" v-model="blog.content"></textarea>
      <div id="checkboxs">
        <label for>Vue.js</label>
        <input type="checkbox" value="Vue.js" v-model="blog.categories">
        <label for>Node.js</label>
        <input type="checkbox" value="Node.js" v-model="blog.categories">
        <label for>Angela.js</label>
        <input type="checkbox" value="Angela.js" v-model="blog.categories">
        <label for>React.js</label>
        <input type="checkbox" value="React.js" v-model="blog.categories">
      </div>
      <label for>作者：</label>
      <select v-model="blog.auther">
        <option v-for="auther in authers">{{auther}}</option>
      </select>
      <input id="fabu" type="button" v-on:click="sendBlog" value="发布微博">
    </form>
    <div>
      <h1 v-if="kaiguan">发送成功</h1>
    </div>

    <hr>

    <div id="preview">
      <h3>博客总览</h3>
      <p>博客标题:{{blog.title}}</p>
      <p>博客内容</p>
      <p>博客分类</p>
      <ul>
        <li v-for="categorie in blog.categories">{{categorie}}</li>
      </ul>
      <p>作者：{{blog.auther}}</p>

      <p>{{blog.content}}</p>
    </div>
  </div>
</template>
<script>
export default {
  name: "blog",
  data() {
    return {
      blog: {
        title: "",
        content: "",
        categories: [],
        auther: ""
      },
      authers: ["Harry", "Zhangsan", "Lisi"],
      kaiguan: false
    };
  },
  methods: {
    sendBlog: function() {
      this.$http
        .post("http://jsonplaceholder.typicode.com/posts", {
          title: this.blog.title,
          body: this.blog.content,
          userId: 1
        })
        .then(function(data) {
          console.log(data);
        });
      this.kaiguan = !this.kaiguan;
    }
  }
};
</script>
<style scoped>
* {
  box-sizing: border-box;
}
#add-blog {
  margin: 20px auto;
  max-width: 600px;
  padding: 20px;
}
label{
  display: block;
  margin: 20px 0 10px;
}
input[type=text],textarea,select{
 display: block;
 padding: 8px;
 width: 100%；
}
#checkboxs label{
  display: inline-block;
}
#checkboxs input{
  display: inline-block;
  margin-right:5px;

}
#fabu{
  display: block;
  margin: 20px 0;
  background: crimson;
  color: #fff;
  border:0;
  padding:14px;
  border-radius: 4px;
  font-size: 18px;
  cursor: pointer;
}
#preview{
  padding: 10px 20px;
  border: 1px #ccc dotted;
  margin:30px 0;

}
h3{
  margin-top:10px 
}
</style>
