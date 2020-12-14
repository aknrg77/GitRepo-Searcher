<template>
    
<div>

<div class="searchBox">
  <input class="searchInput" v-model="value" type="text" placeholder="Search">
    <button v-on:click="findUsers" class="searchButton" href="#">
      <i class="fas fa-search"></i>
    </button>
</div>




<div class="button_cont">
  <button class="button-success" v-on:click="findRepo">Repos</button>
</div>
    


<div class="Repolist" v-show="this.repoclicked">
  <h3>Repositories</h3>
  <li v-for="item in list" :key="item.id">
    <a v-bind:href="item.html_url">{{item.name}}</a>
  </li>
</div>


<div class="profile" v-show="this.clicked">
    <div class = "gradient-border" id="box" >
        <img v-bind:src="this.avatar_url" width="300px" height="300px" >
    </div>
</div>


</div>

</template>


<script>

import axios from 'axios';
//import SearchBox from './SearchBox';


export default {
    name : 'Home',

    data(){
        return {
                value : '',
                list : [],
                avatar_url : '',
                clicked: false,
                repoclicked: false
        }
    },

    methods : {

      async findUsers(){

      try{
          if(this.value!=undefined){
              let url = 'https://api.github.com/search/users?q=' + this.value;
              const res = await axios.get(url);
              this.avatar_url = res.data.items[0].avatar_url;
              this.clicked = true;

              window.open(res.data.items[0].html_url,"_blank");
              this.repoclicked =  false;
              
          }
      }catch(err){
          console.log(err);
      }
      },


      async findRepo(){

        try{
            if(this.value!=undefined){
                
                let url = 'https://api.github.com/users/' + this.value + '/repos';
              
                const repo = await axios.get(url);

                this.list = repo.data;

                this.repoclicked= true;


            }
        }catch(err){
            console.log(err);
        }
      }
    }

}
</script>


<style scoped>



.searchBox {
    position: absolute;
    top: 25%;
    left: 50%;
    transform:  translate(-50%,50%);
    background: #2f3640;
    height: 40px;
    border-radius: 40px;
    padding: 10px;

}

.searchBox:hover > .searchInput {
  width: 240px;
  padding: 0 6px;
}

.searchBox:hover > .searchButton {
  background: white;
  color : #2f3640;
}

.searchButton {
  color: white;
  float: right;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  background: #2f3640;
  display: flex;
  justify-content: center;
  align-items: center;
  transition: 0.4s;
}

.searchInput {
  border:none;
  background: none;
  outline:none;
  float:left;
  padding: 0;
  color: white;
  font-size: 16px;
  transition: 0.4s;
  line-height: 40px;
  width: 0px;

}

@media screen and (max-width: 620px) {
.searchBox:hover > .searchInput {
    width: 150px;
    padding: 0 6px;
}
}
.button_cont{
  position:absolute;
  top:35%;
  left: 0;
  right: 0;
  margin: auto;
  display: flex;
  margin: 60px auto;
  flex-wrap: wrap;
  justify-content: center;
}

.Repolist{
  position: absolute;
  margin-top: 1%;
  left:2%;
    
}

.button-success {
  background: rgb(28, 184, 65);
  color: white;
  border-radius: 4px;
  text-shadow: 0 1px 1px rgba(0, 0, 0, 0.2);
  font-size: 110%;
}

.profile{
    margin-top: 3%;
    margin-right: 3%;
    float : right;
    
}
.image{
    border : 3px solid black;
}

#box {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 300px;
  height: 300px;
  color: white;
  font-family: 'Raleway';
  font-size: 2.5rem;
}
.gradient-border {
  --borderWidth: 4px;
  background: #1D1F20;
  position: relative;
  border-radius: var(--borderWidth);
}
.gradient-border:after {
  content: '';
  position: absolute;
  top: calc(-1 * var(--borderWidth));
  left: calc(-1 * var(--borderWidth));
  height: calc(100% + var(--borderWidth) * 2);
  width: calc(100% + var(--borderWidth) * 2);
  background: linear-gradient(60deg, #f79533, #f37055, #ef4e7b, #a166ab, #5073b8, #1098ad, #07b39b, #6fba82);
  border-radius: calc(2 * var(--borderWidth));
  z-index: -1;
  animation: animatedgradient 3s ease alternate infinite;
  background-size: 300% 300%;
}


@keyframes animatedgradient {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}



</style>