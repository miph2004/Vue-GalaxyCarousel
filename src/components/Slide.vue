 <template>
 <li
    ref="li"
    :aria-hidden="!isCurrent"
    :tabIndex="-1"
    :aria-labelledby="id"
    class="Slide"
    :style="`background-image: url(` + image + `)`"
 >
  <div class="SlideContent">
    <h2 id="id" style="margin-bottom: 2rem">{{title}}</h2>
    <p>{{content}}</p>
  </div>
 </li> 
</template>

<script>
export default {
  name: "Slide",
  props: ["isCurrent", "takeFocus", "image", "id", "title", "content"],
  mounted() {
    if(this.isCurrent && this.takeFocus) {
      this.$refs["li"].focus()
    }
  },
  updated() {
    if(this.isCurrent && this.takeFocus) {
      this.$refs["li"].focus()
    }
  }
}
</script>