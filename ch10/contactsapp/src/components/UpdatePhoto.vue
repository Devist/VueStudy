<template>
  <div class='modal'>
    <div class='form' @keyup.esc='cancelEvent'>
      <form method='post' enctype='multipart/form-data'>
        <h3 class='heading'>:: 사진 변경</h3>
        <input type='hidden' name='no' class='long' disabled v-model='contact.no'>
        <div>
          <label>현재 사진</label>
          <img class='thumb' :src='contact.photo'>
        </div>
        <div>
          <label>사진 파일 선택</label>
          <label>
            <input ref='photofile' type='file' name='photo' class='long btn btn-default'>
          </label>
        </div>
        <div>
          <div>&nbsp;</div>
          <input type='button' class='btn btn-primary' value='변 경' @click='photoSubmit()'>
          <input type='button' class='btn btn-primary' value='취 소' @click='cancelEvent'>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import eventBus from "../EventBus.js"

export default {
  name: "updatePhoto",
  props: ["contact"],
  methods: {
    cancelEvent: function() {
      eventBus.$emit("cancel")
    },
    photoSubmit: function() {
      var file = this.$refs.photofile.files[0]
      eventBus.$emit("updatePhoto", this.contact.no, file)
    }
  }
}
</script>
