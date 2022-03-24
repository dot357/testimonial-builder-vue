<template>
  <div>
    <div class="input-box">
     
      <div class="input-field content-field">
      <label for="import"> 
          Please add <strong>###</strong> seperated values 
          <br>
          <p style="font-size:0.8rem;margin-top:15px;">
              TITLE<strong>###</strong>CONTENT<strong>###</strong>SHOPPING_PLATFORM
          </p>
      </label>
      <textarea
        id="import"
        placeholder="Import data"
        v-model="importData"
      ></textarea>
    </div>

      <div class="buttons">
       
      <button class="add-more btn-normal" :disabled="!importData" @click="importer">Import</button>
      <button class="add-more btn-normal" @click="this.$emit('close-bulk-import', false)">Close</button>
    </div>
    </div>
  </div>
</template>

<script>
import { useToast } from "vue-toastification";
export default {
  data() {
    return {
      importData : null
    };
  },
  methods : {
      importer(){
          let lines = this.importData.split('\n')
          this.importData = null
          let splited = []
          lines.forEach(element => {
            element = element.split('###')
            splited.push({
                title : element[0],
                content : element[1],
                place : element[2]
            })
          });

          
          this.$emit('bulk-imported', splited)

           const toast = useToast();
                toast.success("Successfully Imported", {
                timeout: 2000,
                });


            

      }
  }
};
</script>

<style scoped>
.input-box {
  width: 100%;
  height: 100%;
  background: rgb(255, 255, 255);
  display: flex;
  flex-direction: column;

  padding: 1rem;
  gap: 13px;
}

textarea {
  height: 450px;
 
}


.content-field {
  height: auto;
  min-height: 50%;
}

.buttons{
    display: flex;
    flex-direction: column;
    gap: 13px;
}
</style>
