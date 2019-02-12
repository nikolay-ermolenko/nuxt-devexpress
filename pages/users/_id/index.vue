<template>
  <div class="user">
    <div class="dx-fieldset form">
      <div class="dx-field">
        <div class="dx-field-label">Name</div>
        <div class="dx-field-value-static">
          <p>
            <span id="subject1">{{ name }}</span>
          </p>
        </div>
      </div>
      <div class="dx-field">
        <div class="dx-field-label">User name</div>
        <div class="dx-field-value-static">
          <p>
            <span id="subject1">{{ username }}</span>
          </p>
        </div>
      </div>
      <div class="dx-field">
        <div class="dx-field-label">Email</div>
        <div class="dx-field-value-static">
          <p>
            <span id="subject1">{{ email }}</span>
          </p>
        </div>
      </div>
      <div class="dx-field">
        <div class="dx-field-label">Phone</div>
        <div class="dx-field-value-static">
          <p>
            <span id="subject1">{{ phone }}</span>
          </p>
        </div>
      </div>
      <div class="dx-field">
        <div class="dx-field-label">Website</div>
        <div class="dx-field-value-static">
          <p>
            <span id="subject1">{{ website }}</span>
          </p>
        </div>
      </div>
    </div>
    <nx-toolbar />
  </div>
</template>

<script>
import axios from 'axios'
import NxToolbar from '~/components/Toolbar.vue'

export default {
  components: {
    NxToolbar
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
.dx-field-value-static {
  text-align: left;
}
</style>
