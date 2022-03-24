<template>
  <section class="main">
    
    <!--
      > Input fields
      > Display area
      > HTML Output

     -->
     <button class="export btn-normal" @click="exportToHtml">Export to html</button>

    <div class="left">
      
       <Input v-if="!show.bulkImport" @object-saved="gatherData($event)"  @initiate-bulk-import="this.show.bulkImport=$event"/>
       <BulkImport v-if="show.bulkImport" @close-bulk-import="this.show.bulkImport=$event" @bulk-imported="testimonialObject = $event" />
       
    </div>

    <div class="right">
      <font-awesome-icon icon="user-secret" />

      <ListViewer :obj="testimonialObject"/>
    </div>
    
    

  </section>
</template>

<script>
import Input from './components/Input.vue'
import BulkImport from './components/BulkImport.vue'
import ListViewer from './components/ListViewer.vue'
import { useToast } from "vue-toastification";
export default {
  data () {
    return {
      testimonialObject : [],
      show : {
        bulkImport : false
      }
    }
  },
 components:{
   Input,
   BulkImport,
   ListViewer
 },
 methods : {
   gatherData($event){
     
     this.testimonialObject = $event
   },
   exportToHtml(){
     //solutionTwo
     // navigator.clipboard.writeText(value);
     let value = ''
     this.testimonialObject.forEach(e => {
       value += `
        <div class="singleReview">
          <div class="header">
            <div class="reviewStars">
              <i class="fas fa-star" aria-hidden="true"></i
              ><i class="fas fa-star" aria-hidden="true"></i
              ><i class="fas fa-star" aria-hidden="true"></i
              ><i class="fas fa-star" aria-hidden="true"></i
              ><i class="fas fa-star" aria-hidden="true"></i>
            </div>
            <p>
              <strong> <abbr title="${e.place}">${e.title}</abbr> </strong>
            </p>
          </div>
          <div class="content">
            <p>
              ${e.content}
            </p>
          </div>
      </div>
       `
     })

     navigator.clipboard.writeText(value);

     const toast = useToast();
        toast.success("Content coppied", {
          timeout: 2000,
        });

     
   
   }
 },
 watch : {
   testimonialObject(value, oldValue) {
     console.log(value, oldValue);
   }
 }
 
};
</script>


<style scoped>

.main {
  width: 100%;
  height: 100vh;
  
  display: flex;
  flex-direction: row;
  align-items: flex-start;
  gap: 25px;
}
.left{
  width: 600px;
  height: 100vh;
 
  
}

.right{
  width: 100%;
  height: 100%;
  padding: 2rem;
  display: flex;
  flex-direction: row;
  overflow-x: overlay;
  box-shadow: inset 0px 0px 25px 0px rgba(0, 0, 0, 0.185);
}


.export{
  position: fixed;
  width: 30%;
  background: white;
  bottom: 2rem;
  right: 2rem;
  z-index: 99;
}

</style>