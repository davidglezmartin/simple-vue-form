<template>
    <form @submit.prevent="postForm()">
        <slot></slot>
    </form>
</template>

<script>
import axios from 'axios'

export default {
  name: 'simple_vue_form',
  data () {
    return {
      trueTags: ['input', 'textarea', 'select'],
      notInputTypes: ['submit', 'reset', 'button'],
      dataForm: {}
    }
  },
  props: ['action', 'config'],
  methods: {
    postForm () {
      const form = document.querySelector('form').childNodes
      form.forEach(param => {
        if (this.trueTags.indexOf(param.tag) && this.notInputTypes.indexOf(param.type) === -1 && param.value !== undefined) {
          this.dataForm[param.name] = param.value
        }
      })
      this.post()
    },
    post () {
      if (this.config.ajax) {
        this.ajaxPost()
      }
      if (this.config.formData) {
        this.postData()
      }
    },
    postData () {
      this.$emit('dataForm', this.dataForm)
    },
    ajaxPost () {
      axios.post(this.action, this.dataForm).then(response => {
        this.$emit('ajaxSuccess', response)
      }).catch(error => {
        this.$emit('ajaxError', error)
      })
    }
  }
}
</script>
