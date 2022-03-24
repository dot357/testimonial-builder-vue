<template>
  <!-- INPUT -->
  <div class="input-box" >
  

    <div class="input-field">
      <label for="title"> Title</label>
      <input id="title" type="text" placeholder="Title" v-model="input.title" />
    </div>

     <div class="input-field">
      <label for="place"> Shopping platform</label>
      <input id="place" type="text" placeholder="Title" v-model="input.place" />
    </div>


    <div class="input-field content-field">
      <label for="content"> Content</label>
      <textarea
        id="content"
        placeholder="Content"
        v-model="input.content"
      ></textarea>
    </div>

    <div class="buttons">
      <button class="add-more btn-normal" @click="addMore">Add More</button>
      <button class="add-more btn-normal" @click="initiateBulkImport">Bulk import</button>
      <div class="bottom-buttons">
        <button class="add-more btn-normal" @click="saveTemplate">
          Save template
        </button>
        <button
          class="add-more btn-normal"
          :disabled="!isTemplate"
          @click="loadFromTemplate"
          :style="{
            backgroundColor: isTemplate ? 'black' : 'white',
            color: isTemplate ? 'white' : 'black',
          }"
        >
          Load from template
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props:{
    collectedTestimonialObject : {
      type : Object,
      default : []
    }
  },
  data() {
    return {
      isTemplate: false,
      input: {
        title: null,
        place : null,
        content: null,
      },
      testimonialsData: [
        {
          id: 1,
          place : 'Amazon',
          title: "Name Surname",
          content: "Lorem ipsum dolor sit amed.",
        },
      ],
    };
  },
  created() {
    this.$emit("object-saved", this.testimonialsData);
  },
  mounted() {
    this.isTemplate = this.isTemplateExists();
    console.log(this.isTemplate);
  },
  methods: {
    addMore() {
      const obj = {
        id: this.testimonialsData
          ? this.testimonialsData[this.testimonialsData.length - 1].id + 1
          : 1,
        place : this.input.place,
        title: this.input.title,
        content: this.input.content,
      };
      this.testimonialsData.push(obj);
      this.$emit("object-saved", this.testimonialsData);
    },
    saveTemplate() {
      window.localStorage.setItem(
        "template",
        JSON.stringify(this.testimonialsData)
      );
      this.$emit("object-saved", this.testimonialsData);
      this.isTemplate = this.isTemplateExists();
    },
    loadFromTemplate() {
      const data = JSON.parse(window.localStorage.getItem("template"));
      this.testimonialsData = data;
      this.$emit("object-saved", this.testimonialsData);
    },
    isTemplateExists() {
      let bool = false;
      const data = JSON.parse(window.localStorage.getItem("template"));
      data ? (bool = true) : (bool = false);
      return bool;
    },
    initiateBulkImport(){
        
       this.$emit('initiate-bulk-import', true)
    }
  },
   watch : {
   collectedTestimonialObject(value) {
     this.testimonialsData = value
   }
 }
};
</script>

<style scoped>




.buttons {
  display: flex;
  flex-direction: column;
  gap: 15px;
  margin-top: auto;
}

.bottom-buttons {
  display: flex;
  flex-direction: row;
  gap: 15px;
  align-items: center;
}

.bottom-buttons > button {
  width: 100%;
}
textarea {
  height: 100%;
}


.content-field {
  height: auto;
  min-height: 50%;
}
</style>
