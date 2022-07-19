<template>
  <div class="container text-center mt-5 mb-5">
    <h1 class="mt-5 fw-bolder text-success">Peter Park</h1>
    <h2 class="mt-5 fw-bolder text-warning">Long term parking permits</h2>
    <div class="table-responsive my-5">
      <Table
        :fields="fields"
        :permits="permits"
        :countries="countries"
        :onchange="onchange"
      ></Table>
    </div>
  </div>
</template>

<script>
import Table from "./components/Table.vue";
import "bootstrap/dist/css/bootstrap.min.css";

export default {
  name: "App",
  components: {
    Table,
  },
  setup() {
    // Germany ^[A-ZÄÖÜ]{1,3}\-[ ]{0,1}[A-Z]{0,2}[0-9]{1,4}[H]{0,1}
    // France   /^(?!ss|ww|.[iou]|[iou].)[a-z]{2}[-\s]?\d{3}[-\s]?(?!ss|ww|.[iou]|[iou].)[a-z]{2}$/i
    //
    //An array of values for the data
    const permits = [
      {
        licensePlate: "F-RM373",
        country: "DE",
        startDate: "2022-02-23",
        endDate: "2022-02-23",
        ownerName: "Kanimozhi Duraikannu",
        status: true,
      },
      {
        licensePlate: "AB-123-CD",
        country: "FR",
        startDate: "2022-02-23",
        endDate: "2022-02-23",
        ownerName: "Nivedha Duraikannu",
        status: true,
      },
      {
        licensePlate: "DE12324",
        country: "AU",
        startDate: "2022-02-23",
        endDate: "2022-02-23",
        ownerName: "Clemens Mirbach",
        status: false,
      },
      {
        licensePlate: "WÜ-Z1",
        country: "SW",
        startDate: "2022-02-23",
        endDate: "2022-02-23",
        ownerName: "Kanimozhi Duraikannu",
        status: true,
      },
      {
        licensePlate: "DE12324",
        country: "DE",
        startDate: "2022-02-23",
        endDate: "2022-02-23",
        ownerName: "Meenatchi Duraikannu",
        status: true,
      },
      {
        licensePlate: "FE5467",
        country: "FR",
        startDate: "2022-02-23",
        endDate: "2022-02-23",
        ownerName: "Duraikannu",
        status: false,
      },
      {
        licensePlate: "FFSW234",
        country: "SW",
        startDate: "2022-02-23",
        endDate: "2022-02-23",
        ownerName: "Cedrice",
        status: true,
      },
      {
        licensePlate: "DE12324",
        country: "AU",
        startDate: "2022-02-23",
        endDate: "2022-02-23",
        ownerName: "Clemens Mirbach",
        status: true,
      },
      {
        licensePlate: "TTTT",
        country: "FR",
        startDate: "2022-02-23",
        endDate: "2022-02-23",
        ownerName: "Kanimozhi Duraikannu",
        status: true,
      },
    ];

    const fields = [
      {
        label: "License Plate",
        property: "licensePlate",
        columnType: "input",
        onchange: "onChange()",
      },
      {
        label: "Country",
        property: "country",
        columnType: "country",
        onchange: "onChange",
      },
      {
        label: "Start Date",
        property: "startDate",
        columnType: "date",
        onchange: "onChangeStartDate",
      },
      {
        label: "End Date",
        property: "endDate",
        columnType: "date",
        onchange: "onChangeEndDate",
      },
      {
        label: "Owner Name",
        property: "ownerName",
        columnType: "ownerName",
        onchange: "onChangeOwnerName($event)",
      },
      {
        label: "Status",
        property: "status",
        columnType: "status",
        onchange: "onChangeStatus",
      },
    ];
    const countries = [
      { value: "DE", label: "Germany" },
      { value: "FR", label: "France" },
      { value: "SW", label: "Switzerland" },
      { value: "AU", label: "Austria" },
      { value: "", label: "Other" },
    ];
    const onchange = (e, val) => {
      console.log(e);
      console.log(val);
      console.log("Test");
    };
    return { permits, fields, countries, onchange };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
