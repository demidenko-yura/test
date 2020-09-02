<template>
  <div id="app">
    <Form />
  </div>
</template>

<script>
import Form from './components/Form.vue'

export default {
  name: 'App',
  components: {
    Form
  }
};
</script>

<style lang='sass'>
#app 
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50; 

.block
  display: flex;
  flex-direction: column;

.block_document
  display: block;
  width: 100%;
  text-align: left;  

  input 
    width: 50%;

    @media screen and (max-width: 778px)
      width: auto;    


.result
  display: flex;
  flex-wrap: wrap;


.label
  font-size: 25px;
  display: flex;
  margin-left: 10px;
  margin-top: 25px; 

.errorClass
  border: 1px solid red; 




form 
  display: flex;
  flex-direction: column;
  margin-bottom: 50px;

input 
  height: 30px;
  font-size: 20px;
  padding: 10px;
  margin: 10px;
  outline: none;

span 
  display: flex;
  align-items: center;
  font-size: 20px;


select 
  display: block;
  margin: 10px 10px;
  width: 40%;
  font-size: 20px;
  max-height: 77px;

  @media screen and (max-width: 750px)
    width: auto;


button 
  display: block;
  height: 40px;
  border-radius: 20px;
  border: none;
  background: #1e90ff;
  margin: 0 auto;
  font-size: 20px;
  outline: none;
  cursor: pointer;
  padding: 5px 10px;


button:hover 
  opacity: 0.9;


ul 
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: 35%;
  margin: 10px auto;
  text-align: left;
  border: 2px solid #2c3e50;

  li:last-child
    margin-bottom: 20px;

  @media screen and (max-width: 750px)
    width: 70%;

    li
      margin: 0 10px;

b
  color: red;
  margin-left: 5px;

</style>
