<template>

  <v-container fluid class="mx-3 white elevation-1" style="max-width: calc(100vw - 32px)">

    <v-btn x-large to="/admin/ApplicationUser" color="primary">
      Application User Admin Table
    </v-btn>

    <v-divider class="mt-4"></v-divider>

    Below is a very simple example of using components from coalesce-vue-vuetify to 
    display and edit properties of a model. Autosave is enabled.

    <c-loader-status 
      #default 
      :loaders="{
        'no-error-content no-intial-content': [user.$load],
        '': [user.$save],
      }"
    >
      <div class="title py-2">
        Editing User ID: <c-display :model="user" for="applicationUserId" />
      </div>
      <c-input :model="user" for="name" />
    </c-loader-status>
  </v-container>
</template>

<script lang="ts">
  import { Component, Prop, Vue } from 'vue-property-decorator';
  import { ApplicationUserViewModel } from '@/viewmodels.g';

@Component
export default class HelloWorld extends Vue {
  @Prop() private msg!: string;

  private user = new ApplicationUserViewModel();

  async mounted() {
    await this.user.$load(1);
    this.user.$startAutoSave(this, { wait: 500 })
  }
}
</script>
