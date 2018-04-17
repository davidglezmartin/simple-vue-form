# Simple Vue Form

A Vue.js component for make ajax form ease.

## Install

``` bash
$ npm i simple-vue-form
```
## Usage
You must specify a post url in action="" like conventional html5 form, also you must specify a "data", "success" and "error" function for receive the data and ajax responses.

####Config
```json
config: {
  ajax: true, //if you want use a integrated ajax
  formData: true //if you want receive the data of form
}
```
####Example
```html
<template>
    <simple-vue-form action="/posts" 
    :config="config" 
    @dataForm="dataForm"  
    @ajaxSuccess="formSuccess" 
    @ajaxError="formError">
      <input name="title"/>
      <textarea name="body"></textarea>
      <input type="submit"/>
    </simple-vue-form>
</template>

<script>
import simpleVueForm from 'simple-vue-form'

export default {
  data () {
    return {
      config: {
        ajax: true,
        reactiveData: true
      }
    }
  },
  components: {
    'simple-vue-form': simpleVueForm
  },
  methods: {
    formSuccess (response) {
      // response of the success ajax post
    },
    formError (response) {
      // response of the fail ajax post
    },
    dataForm (data) {
      // only the object of the form data responds
    }
  }
}
</script>
```
#### The json request post looks like

```
{
    'title': 'Awesome Post',
    'body': 'Lorem ipsum dolor sit amet.'
}
