<template>
  <section class="wrapper" v-for="single in obj" :key="single.id">

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
  props: {
    obj: {
      type: Object,
      default: [],
    },
  },
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
}
</style>