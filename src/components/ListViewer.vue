<template>
  <section class="wrapper" v-for="single in obj" :key="single.id">

    <div class="singleReview">
      <span class="delete-button" @click="deleteItem(single.id)">X</span>
      
      <div class="header">
        <div class="reviewStars">
          <i class="fas fa-star" aria-hidden="true"></i
          ><i class="fas fa-star" aria-hidden="true"></i
          ><i class="fas fa-star" aria-hidden="true"></i
          ><i class="fas fa-star" aria-hidden="true"></i
          ><i class="fas fa-star" aria-hidden="true"></i>
        </div>
        <p>
          <strong> <abbr :title="single.place">{{single.title}}</abbr> </strong>
        </p>
      </div>
      <div class="content">
        <p>
           "{{single.content}}"
        </p>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {};
  },
  emits: ["item-delete"],
  props: {
    obj: {
      type: Object,
      default: [],
    },
  },
  methods : {
    deleteItem(id){
      this.$emit('item-delete', id)
    }
  }
};
</script>


<style scoped>
.wrapper{
    position: relative;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    gap: 5px;
    justify-content: center;
    align-items: center;
    width: 100%;
}

.singleReview{
    background: white;
    padding: 1em 2em;
    text-align: justify;
    line-height: 35px;
    border-radius: 4px;
    min-height: 250px;
    min-width: 250px;
    display: flex;
    flex-direction: column;
    width: 100%;
    align-items: center;
    text-align: center;
    box-shadow: 0 10px 7px #0000000d;
    margin: 1em;
    position: relative;
}

.delete-button{
  width: 25px;
  height: 25px;
  border-radius: 50%;
  background-color: black;
  color: white;
  font-weight: bold;
  cursor: pointer;
  position: absolute;
  right: -7px;
  top: -15px;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
}



.delete-button:hover{
  transition: opacity transform 0.3s ease;
  transform: scale(0.95);
  opacity: 0.8;
}
</style>