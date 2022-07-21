<template>
  <div class="searchBar">
    <!-- Filter Search -->
    <div class="input-group mb-5">
      <input
        type="search"
        class="form-control"
        v-model="searchQuery"
        placeholder="Search by Number plate / Vechile owner name"
        aria-label="Recipient's username"
        aria-describedby="button-addon2"
      />
    </div>
  </div>

  <table id="tableComponent" class="table table-bordered table-striped">
    <thead>
      <tr>
        <th
          v-for="field in fields"
          :key="field.property"
          @click="sortTable(field.property)"
        >
          {{ field.label }}
          <i class="bi bi-sort-alpha-down" aria-label="Sort Icon"></i>
        </th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="item in filterItems" :key="item">
        <td v-for="field in fields" :key="field.property">
          <div v-if="field.columnType === 'date'">
            <input
              @change="onchange(item, field.property)"
              type="date"
              format="dd-MM-yyyy"
              v-model="item[field.property]"
            />
          </div>
          <div v-else-if="field.columnType === 'status'">
            <input
              @change="onchange(item, field.property)"
              type="checkbox"
              v-model="item[field.property]"
            />
            <div v-if="field.changed === true">
              <button variant="success"   @click="onsave(item)">Save</button>
              <button variant="success"   @click="ondelete(item)">Delete</button>            </div>
          </div>
          <div v-else-if="field.columnType === 'country'">
            <select
              @change="onchange(item, field.property)"
              class="form-control"
              :required="true"
              v-model="item[field.property]"
            >
              <option
                v-for="option in countries"
                v-bind:value="option.value"
                v-bind:key="option.value"
              >
                {{ option.label }}
              </option>
            </select>
          </div>
          <div v-else>
            <input
              class="form-control"
              type="text"
              v-model="item[field.property]"
              @change="onchange(item, field.property)"
            />
          </div>
        </td>
      </tr>
    </tbody>
  </table>
</template>
<script>
import { computed, ref } from "vue";
import { sortBy } from "lodash";

export default {
  name: "TableComponent",
  props: {
    permits: {
      type: Array,
    },
    fields: {
      type: Array,
    },
    countries: {
      type: Array,
    },
    onchange: {
      type: Function,
    },
     onsave: {
      type: Function,
    },
     ondelete: {
      type: Function,
    },
  },

  setup(props) {
    let sort = ref(false);
    let updatedList = ref([]);
    let searchQuery = ref("");

    const sortTable = (col) => {
      sort.value = !sort.value;
      updatedList.value = sortBy(props.permits, col);
    };

    const sortItems = computed(() => {
      if (sort.value) {
        return updatedList.value;
      } else {
        return props.permits;
      }
    });
    const filterItems = computed(() => {
      return sortItems.value.filter((product) => {
        return (
          product.licensePlate
            .toLowerCase()
            .indexOf(searchQuery.value.toLowerCase()) != -1 ||
          product.ownerName
            .toLowerCase()
            .indexOf(searchQuery.value.toLowerCase()) != -1
        );
      });
    });

    return { sortItems, sortTable, searchQuery, filterItems };
  },
};
</script>
<style scoped>
table th:hover {
  background: #f2f2f2;
}
</style>
