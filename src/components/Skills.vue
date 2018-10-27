<template>
  <div class="hello">
    <div class="holder">
      <form @submit.prevent="addSkill">
        <div class="form-group">
          <input class="form-control bg-dark text-white" type="text" placeholder="Enter your skill." v-model="skill" v-validate="'required|min:5'" name="skill">

          <transition name="alert-in" enter-active-class="animated flipInX" leave-active-class="animated flipOutX">
            <p class="alert alert-danger" v-if="errors.has('skill')">{{ errors.first('skill') }}</p>
          </transition>
        </div>
        <!-- <button class="btn btn-primary">Add</button> -->
      </form>

      <ul class="list-group">
        <transition-group name="list" enter-active-class="animated bounceInUp" leave-active-class="animated bounceOutDown">
          <li class="list-group-item" v-for="(skillObj, index) in skills" :key="index">
            {{ skillObj.skill }}
            <i class="fas fa-minus-circle" @click="deleteSkill(index)"></i>
          </li>
        </transition-group>
      </ul>
      <p class="text-center bg-light p-4">Your skills</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Skills',
  data(){
    return{
      skills: [
        {"skill": "Vue.js"},
        {"skill": "Java"},
      ],
      skill: '',
    }
  },
  methods: {
    addSkill(){
      this.$validator.validateAll().then(result => {
        if(result){
          this.skills.push({skill: this.skill});
          this.skill = '';
        }else{
          console.log('Not valid skill');
        }
      })

    },
    deleteSkill(index){
      this.skills.splice(index, 1);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import "https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.7.0/animate.css";

  .alert-in-enter-active {
    animation: bounce-in .5s;
  }
  .alert-in-leave-active {
    animation: bounce-in .5s reverse;
  }
  .fa-minus-circle {
    color: red;
    float: right;
    cursor: pointer;
  }

  @keyframes bounce-in {
    0% {
      transform: scale(0);
    }
    50% {
      transform: scale(1.5);
    }
    100% {
      transform: scale(1);
    }
  }
</style>
