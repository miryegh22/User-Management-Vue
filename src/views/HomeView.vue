<template>
  <div class="home">
    <UserTable />
  </div>
</template>

<script>
import UserTable from '@/components/UserTable.vue';

export default {
  name: 'HomeView',
  components: {
    UserTable
}
}
</script>
