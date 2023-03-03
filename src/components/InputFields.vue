<template>
  <div>
    <b-row>
      <b-col cols="11" class="pr-0">
        <b-form-textarea
            id="textarea-no-resize"
            placeholder="Текстовое поле с фиксированной высотой"
            rows="3"
            no-resize
        ></b-form-textarea>
      </b-col>
      <b-col class="p-0">
        <b-button class="btnAllBlock" block variant="primary">Отправить</b-button>
      </b-col>
    </b-row>


  </div>
</template>

<script>
export default {
  name: "InputFields",
  props: {
    userList: Object
  }
}
</script>

<style scoped>
button.btnAllBlock {
  width: 100%;
  height: 100%;
  display: block;
  position: relative;
}
</style>