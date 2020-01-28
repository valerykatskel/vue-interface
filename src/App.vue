<template>
  <div id="main-app" class="container">
    <h4>{{ title }}</h4>
    <font-awesome-icon icon="plus" class="mr-2"/> Add appointment
  </div>
</template>

<script>
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'

export default {
  name: 'MAinApp',
  data() {
    return {
      title: 'Appointment list'
    }
  },
  components: {
    FontAwesomeIcon
  }
}
</script>

