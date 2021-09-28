<template>
  <div class="project" :class="{complete: this.project.complete}">
      <div class="actions" >
          <h3 @click="showDetails = !showDetails">{{ project.title }}</h3>
          <div class="icons">
              <span class="material-icons" @click="deleteProject">delete</span>
                            <span class="material-icons">edit</span>
              <span class="material-icons" :class="{tick:this.project.complete}" @click="toggleComplete">done</span>

          </div>
      </div>
      <div class="details" v-if="showDetails">
          <p>{{ project.details}}</p>
      </div>
  </div>
</template>

<script>
export default {
    props :['project'],
    data()  {
        return {
            showDetails : false,
            url:'http://localhost:3000/projects/' + this.project.id
        }
    },
    methods:{
        deleteProject(){
            fetch(this.url, { method: 'DELETE' })
                .then(() => this.$emit('delete' , this.project.id))
                .catch(err => console.log(err.message))
        },
        toggleComplete(){
            fetch(this.url,
                {
                method: 'PATCH',
                headers: {'Content-Type':'application/Json',},
                body: JSON.stringify({complete: !this.project.complete})
            })
             .then(() =>{
                 this.$emit('complete', this.project.id)
             })
             .catch((err) =>console.log(err.message))
        }
    }
}
</script>

<style>
    .project {
        margin: 20px auto;
        background: white;
        padding: 10px 20px;
        border-radius: 4px;
        box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.05);
        border-left: 4px solid #e90090;
    }
    h3 {
        cursor: pointer;
    }
    .actions {
        display: flex;
        align-items: center;
        justify-content: space-between;
    }
    .material-icons {
        font-size: 23px;
        margin-left: 10px;
        cursor: pointer;
        color: #bbb;
    }
    .material-icons:hover {
        color: #777;
    }
      .project.complete {
    border-left: 4px solid #00ce99;
  }
  .project.project.complete .tick{
    color:#00ce99;
  }
</style>
