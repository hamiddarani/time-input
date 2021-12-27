<template>
  <div class="hello">
    <input v-model="time" @blur="changeTimePattern"/>
  </div>
</template>

<script>
export default {
  name: 'TimeInput',
  props: {
    value: String
  },
  computed: {
    time: {
      get(){
        if(this.value && this.value.length > 4){
          if(this.value.split(':')[2] === '') return this.value +' :00'
          return this.value.split(':')[0] + ':' + this.value.split(':')[1]
        }
        return this.value
      },
      set(val){
        if(val && val.length === 5){
          this.$emit('input' , `${val}:00`)
          return
        }
        this.$emit('input' , val)
      }
    }
  },
  watch:{
    time(newValue , oldValue){
      
      console.log(this.value)
 
      if((/[a-zA-Z;!@#$%^&*()_-]/).test(newValue)){
        this.time = oldValue
      }

      if((/::/).test(newValue)){
        this.time = oldValue
      }

      if(newValue.length > 5){
        this.time = oldValue
      }

      if(newValue.length === 1 && newValue > 2){
        this.time = '0' + newValue + ':'
      }

      if(newValue.length === 2 && !newValue.includes(':') && newValue.length > oldValue.length){
        this.time = newValue + ':'
      }

      if(newValue > 9 && newValue < 24  && newValue.length === 2 && newValue.length > oldValue.length){
        this.time = newValue + ':'
      }

       if(newValue > 23  && newValue.length > oldValue.length){
        this.time = this.time.slice(0 ,2) + ':' +this.time.slice(2)
      }

      if(newValue > 23 && newValue.length === 2){
        this.time = '00:'
      }

      if(newValue.includes(':') && newValue.split(':')[0] > 23){
        this.time = '00:' + newValue.split(':')[1]
      }

      if(newValue.includes(':') && !newValue.split(':')[0] && !newValue.split(':')[1] && newValue.length > oldValue.length){
        console.log(newValue , oldValue)
        this.time = '00:'
      }

      if(newValue.includes(':') && newValue.split(':')[0].length === 1 && newValue.split(':')[0] > 2){
        this.time = '0' + newValue
      }

      if(newValue.includes(':') && newValue.split(':')[1].length === 1 &&  newValue.split(':')[1] > 5 ){
        this.time =  newValue.split(':')[0] + ':' + '0' + newValue.split(':')[1]
      }

      if(newValue.includes(':') && newValue.split(':')[1].length &&  newValue.split(':')[1] > 59 && newValue.split(':')[1].length === 2){
        this.time =  newValue.split(':')[0] + ':' + '00'
      }

      if(oldValue.includes(':') && newValue[newValue.length - 1] === ':' && newValue.length > oldValue.length){
        this.time = oldValue
      }
    }
  },
  methods: {
    changeTimePattern(){
     

      if(this.time.split(':')[0] && !this.time.split(':')[1] && this.time.split(':')[0].length === 2 ){
        this.time = this.time.split(':')[0] + ':00'
      }

      if(this.time.includes(':') && !this.time.split(':')[0]){
        this.time = '00:' + this.time.split(':')[1]
      }

      if(this.time.includes(':') && !this.time.split(':')[0]){
         this.time = this.time.split(':')[0] + ':00'
      }

      if(this.time.length === 1 && !this.time.includes(':')){
        this.time = '0' + this.time + ':00'
      }

      if(!this.time.split(':')[0].length && this.time.includes(':')){
        this.time = '00' + this.time
      }

      if(!this.time.includes(':') && this.time.length){
        this.time = this.time.slice(0 ,2) + ':' + this.time.slice(2,4)
      }

      if(this.time.includes(':') && this.time.split(':')[1] == 0 ){
        this.time = this.time.split(':')[0] + ':00' 
      }

      if(!this.time.includes(':') && this.time.length  && this.time.length === 3){
        this.time = this.time.slice(0 ,2) + ':' + this.time.slice(2,3) + '0'
      }

      if(this.time.includes(':')  && this.time.split(':')[1].length === 1){
        this.time = this.time.slice(0 ,2) + ':0' + this.time.slice(3) 
      }

      if(this.time.includes(':')  && this.time.split(':')[0].length === 1){
        this.time = '0' + this.time.split(':')[0] + ':' + this.time.split(':')[1] 
      }

      if(this.time.includes(':')  && this.time.split(':')[0].length === 1 && this.time.split(':')[1].length === 1){
        this.time = '0' + this.time.split(':')[0] + ':0' + this.time.split(':')[1] 
      }

      if(!this.time.includes(':') && this.time.length ===1){
        this.time = '0' + this.time + ':00'
      }

      if(!this.time.includes(':') && this.time > 9 && this.time < 24){
        this.time = this.time + ':00'
      }

      if(!this.time.includes(':') && (this.time == '00' || this.time == '01' || this.time == '02') ){
        this.time = this.time + ':00'
      }

      if(this.time.includes(':') && this.time.length === 1 ){
        this.time = '00:00'
      }

      
    }
  }
  
}
</script>















<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
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
