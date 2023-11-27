<template>
  <div class="modal">
    <div class="modal-content">
      <h3>User Information</h3>
      <ul>
        <li>Email: {{ data.email }}</li>
        <li>Password: {{ data.password }}</li>
        <li>Role: {{ data.role }}</li>
        <li>Experience: {{ data.exp }}</li>
        <li>Skills:
        <div class="pill-container">
            <div v-for="skill in data.skills" :key="skill" class="pill">
                {{ skill }}
            </div>
        </div>

        </li>
      </ul>
      <button @click="$emit('close')">Close</button>
    </div>
  </div>
</template>

<script setup>

const props = defineProps({
  data: {
    type: Object,
    required: true
  }
});
</script>

<style scoped>
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal-content {
  display: flex;
  align-items: center;
  flex-direction: column;
  width: 300px;
  min-height: 250px;
  background: white;
  padding: 20px;
  border-radius: 5px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.3);
}

ul {
  list-style: none;
  padding: 0;
}

ul li {
  margin-bottom: 10px;
}

.pill-container {
    justify-content: center;
}

</style>
