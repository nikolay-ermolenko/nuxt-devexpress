<template>
  <div class="container">
    <h2>Users</h2>
    <!-- <ul class="users"> -->
      
      <dx-data-grid
        :data-source="users"
        :columns="columns"
        :show-borders="true"
        :showColumnLines="true"
        :rowAlternationEnabled="true"
        :selection="{ mode: 'single' }"
        :hover-state-enabled="true"
        @selection-changed="onSelectionChanged"
      >
      <dx-column
        :width="100"
        :allow-sorting="false"
        data-field="id"
        caption=""
        cell-template="cellTemplate"
      />
       <div
        slot="cellTemplate"
        slot-scope="user"
      >
       <dx-button icon="card" 
          @click="onButtonClick(user, 'card')" />
        <dx-button icon="edit" 
          @click="onButtonClick(user, 'edit')" />
      </div>
      </dx-data-grid>
      <!-- <li v-for="user in users" :key="user.id">
        <NuxtLink :to="'/users/'+user.id" append>
          {{ user.name }}
        </NuxtLink>
      </li> -->
    <!-- </ul> -->
  </div>
</template>


<script>
import { DxDataGrid, DxColumn } from 'devextreme-vue/data-grid'
import { DxButton } from 'devextreme-vue'
import axios from 'axios'

export default {
  components: {
    DxDataGrid,
    DxColumn,
    DxButton
  },
  data() {
    return {
      columns: ['name', 'email', 'phone', 'website', 'company.name']
    }
  },
  async asyncData() {
    const { data } = await axios.get('https://jsonplaceholder.typicode.com/users')
    return { 
      users: data
    }
  },
   methods: {
    onSelectionChanged({ selectedRowsData }) {

    },
    onButtonClick(e, type) {
      if (e && e.data) {
        if(type === 'card') {
          this.$router.push(`/users/${e.data.id}`)
        }
        if(type === 'edit') {
          this.$router.push(`/users/${e.data.id}/edit`)
        }
      }
    }
  }
}
</script>

<style scoped>
.container {
  text-align: center;
  margin-top: 100px;
  font-family: sans-serif;
}
.users {
  list-style-type: none;
}
.users li a {
  display: inline-block;
  width: 200px;
  border: 1px #ddd solid;
  padding: 10px;
  text-align: left;
  color: #222;
  text-decoration: none;
}
.users li a:hover {
  color: orange;
}
</style>