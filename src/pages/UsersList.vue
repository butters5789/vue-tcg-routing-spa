<template>
  <button @click="saveChanges">Save Changes</button>

  <ul>
    <user-item
      v-for="user in users"
      :key="user.id"
      :name="user.fullName"
      :role="user.role"
    ></user-item>
  </ul>
</template>

<script>
import UserItem from '../components/users/UserItem.vue';

export default {
  components: {
    UserItem,
  },
  inject: ['users'],
  data() {
    return {
      changesSaved: false,
    };
  },
  methods: {
    saveChanges() {
      this.changesSaved = true;
    },
  },
  beforeRouteEnter(to, from, next) {
    console.log('Before Route Enter', to, from);
    next();
  },
  beforeRouteLeave(to, from, next) {
    console.log('Before Route Leave', to, from);

    if (this.changesSaved) {
      next(true);
    } else {
      const verify = confirm('Are you sure you want to leave this page?');
      next(verify);
    }
  },
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 2rem auto;
  max-width: 20rem;
  padding: 0;
}
</style>
