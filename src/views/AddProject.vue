<template>
  <form @submit.prevent="handleSubmit">
    <div class="title" v-if="this.id">Edit Project</div>
    <div class="title" v-else>New Project</div>
      <label >Title :</label>
      <input type="text" required v-model="title">
      <label >Details :</label>
      <textarea required v-model="details"></textarea>
      <button v-if="this.id" @click="handleEdit">Edit Project</button>
      <button v-else @click="handleSubmite">Add Project</button>
  </form>
</template>

<script>
export default {
  props:['id'],
    data(){
        return{
            title: '',
            details: '',
            url: 'http://localhost:3000/projects'
        }
    },
    mounted(){
      this.title=''
      this.details=''
      if(this.id){
        console.log(this.id)
        fetch(this.url +'/'+ this.id)
        .then((res) => res.json())
        .then((data) =>{
          this.title = data.title
          this.details = data.details
        })
      }

    },
    methods:{
        handleSubmite(){
            // console.log(this.title)
            // console.log(this.details )
            let project = {
                title : this.title,
                details: this.details,
                complete: false

            }
            console.log(project)
            fetch(this.url, {
                method: 'POST',
                headers: {'Content-Type' : 'application/json'},
                body: JSON.stringify(project)
            })
             .then(() =>{
                 this.$router.push({name: 'Home'})
             })
             .catch((err) => console.log(err.message))
        },
        handleEdit(){
            let project = {
                title : this.title,
                details: this.details,
            }
            console.log(project)
            fetch(this.url + '/' + this.id, {
                method: 'PATCH',
                headers: {'Content-Type' : 'application/json'},
                body: JSON.stringify(project)
            })
             .then(() =>{
                 this.$router.push({name: 'Home'})
             })
             .catch((err) => console.log(err.message))
        }
    }

}
</script>

<style>
      form {
    background: white;
    padding: 20px;
    border-radius: 10px;
  }
  .title{
    display: block;
    color: rgb(36, 25, 25, 0.733);
    text-transform: uppercase;
    font-size: 16px;
    font-weight: bold;
    letter-spacing: 1.5px;
    margin: auto 0 30px;
  }
    label {
    display: block;
    color: #bbb;
    text-transform: uppercase;
    font-size: 14px;
    font-weight: bold;
    letter-spacing: 1px;
    margin: 20px 0 10px 0
  }
  input {
    padding: 10px;
    border: 0;
    border-bottom: 1px solid #ddd;
    width: 100%;
    box-sizing: border-box;
  }
  textarea {
    border: 1px solid #ddd;
    padding: 10px;
    width: 100%;
    box-sizing: border-box;
    height: 100px;
  }
  form button {
    display: block;
    margin: 20px auto 0;
    background: #00ce89;
    color: white;
    padding: 10px;
    border: 0;
    border-radius: 6px;
    font-size: 16px;
    cursor: pointer;
  }
</style>
