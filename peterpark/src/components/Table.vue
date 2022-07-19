<template>
  <h2>Table</h2>
  <table>
    <thead>
      <tr>
        <th>Column1</th>
        <th>Column2</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>Cell 11</td>
        <td>Cell 12</td>
      </tr>
      <tr>
        <td>Cell 11</td>
        <td>Cell 12</td>
      </tr>
    </tbody>
  </table>
</template>
<script>
export default {
  name: "TableComponent",
};
</script>
<style scoped>
table th:hover {
  background: #f2f2f2;
}
</style>
