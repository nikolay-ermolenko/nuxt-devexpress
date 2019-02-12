<template>
  <dx-toolbar :items="toolbarItems" />
</template>


<script>
import { DxToolbar } from 'devextreme-vue';
import notify from 'devextreme/ui/notify';

export default {
  components: {
    DxToolbar
  },
  computed: {
      mode: function() {
        if (this.$route.path.split('/').pop() === 'edit') {
          return 'edit'
        }
        return 'card'
      },
      toolbarItems: function() {
          return [
            {
                location: "before",
                widget: "dxButton",
                options: {
                    icon: "save",
                    onClick: () => {
                        notify('Card has been saved!');
                    }            
                }
            },
            {
                location: "before",
                widget: "dxButton",
                disabled: this.toggle,
                options: {
                    icon: "undo",
                    onClick: () => {
                        notify('Card has been reverted!');
                    }            
                }
            },
            {
                location: "after",
                widget: "dxButton",
                visible: this.mode !== 'card',
                options: {
                    icon: "card",
                    hint: 'View user card',
                    onClick: () => {
                      const userId = this.$route.params.id;
                      this.$router.push(`/users/${userId}`)                      
                    }                    
                }
            },
            {
                location: "after",
                widget: "dxButton",
                visible: this.mode !== 'edit',
                options: {
                    icon: "edit",
                    hint: 'Edit user',
                    onClick: () => {
                      const userId = this.$route.params.id;
                      this.$router.push(`/users/${userId}/edit`)                      
                    }                    
                }
            },
            {
                location: "after",
                widget: "dxButton",
                options: {
                    icon: "home",
                    hint: 'Users list',
                    onClick: () => {
                       this.$router.push('/');
                    }
                }
            }
        ];
      }
  }
}
</script>