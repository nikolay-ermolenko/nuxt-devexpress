<template>
  <div class="user">
    <div class="dx-fieldset">
      <div class="dx-fieldset-header">Main data</div>
      <div class="dx-field">
        <div class="dx-field-label">Name</div>
        <div class="dx-field-value">
          <dx-text-box :value="name"/>
        </div>
      </div>
      <div class="dx-field">
        <div class="dx-field-label">User Name</div>
        <div class="dx-field-value">
          <dx-text-box :value="username"/>
        </div>
      </div>
      <div class="dx-field">
        <div class="dx-field-label">Email</div>
        <div class="dx-field-value">
          <dx-text-box :value="email"/>
        </div>
      </div>
      <div class="dx-field">
        <div class="dx-field-label">Phone</div>
        <div class="dx-field-value">
          <dx-text-box :value="phone"/>
        </div>
      </div>
      <div class="dx-field">
        <div class="dx-field-label">Website</div>
        <div class="dx-field-value">
          <dx-text-box :value="website"/>
        </div>
      </div>
    </div>   
    <nx-toolbar />
  </div>
</template>

<script>
import { DxTextBox } from 'devextreme-vue';
import notify from 'devextreme/ui/notify';
import axios from 'axios'
import NxToolbar from '~/components/Toolbar.vue'

export default {
  components: {
    NxToolbar,
    DxTextBox
  },
  validate({ params }) {
    return !isNaN(+params.id)
  },
  async asyncData({ params, error }) {
    try {
      const { data } = await axios.get(`https://jsonplaceholder.typicode.com/users/${+params.id}`)      
      return data
    } catch (e) {
      error({ message: 'User not found', statusCode: 404 })
    }
  }
}
</script>

<style scoped>
.user {
  text-align: center;
  font-family: sans-serif;
  width: 60%;
  margin: auto;
  max-width: 700px;
}
.dx-field-label {
  text-align: right;
}
</style>
