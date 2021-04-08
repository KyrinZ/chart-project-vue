<template>
  <div class="table-container">
    <table class="table">
      <thead>
        <tr>
          <th>ID</th>
          <th>First Name</th>
          <th>Last Name</th>
          <th>Gender</th>
          <th>Country</th>
        </tr>
      </thead>
      <tbody>
        <tr
          :style="{ backgroundColor: item.favourite_color }"
          v-for="item in data"
          :key="item.id"
        >
          <td>{{ item.id }}</td>
          <td>{{ item.first_name }}</td>
          <td>{{ item.last_name }}</td>
          <td>{{ item.gender }}</td>
          <td>{{ item.country }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "Table",
  props: ["data"],
};
</script>

<style>
.table-container {
  position: relative;
  height: 50vh;
  overflow: scroll;
}
th {
  color: rgb(97, 97, 97);
}
table {
  width: 100%;
}

td {
  text-align: center;
  padding: 0.5rem;
}
</style>
