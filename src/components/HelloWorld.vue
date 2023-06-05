<template>
  <div class="hello">
    <header>
      MY Configuration
    </header>
    <section>
      <form>
        <h3>title</h3>
        <p>paragraph</p>
        <table>
          <thead>
            <tr>
              <th><input type="checkbox" v-model="selectAll" @click="toggleAll"></th>
              <th>Select All</th>
              <th></th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="field in fields" :key="field.name">
              <td><input type="checkbox" v-model="field.selected" @change=toggleField></td>
              <td>{{field.name}}</td>
              <td v-html="field.description"></td>
            </tr>
          </tbody>
        </table>
      </form>
      <button @click="showFields">Save</button>
    </section>
  </div>
</template>


<script>
import { toRaw } from 'vue';
export default {
  name: 'HelloWorld',
  data() {
    return {
      fields: [{
        selected: false,
        name: 'field Name 1',
        description: 'field description 1',
      },
      {
        selected: false,
        name: 'field Name 3',
        description: 'field description 2',
      },
      {
        selected: false,
        name: 'field Name 3',
        description: 'field description 3',
      }
    ],
      selectAll: false,
    };
  },
  computed: {
    amountSelected() {
      const selectedFields = this.fields.filter((field) => field.selected).length;
      if (!selectedFields) return 'none';
      if (selectedFields === Object.keys(this.fields).length) return 'all';
      return 'some';
    }
  },
  methods: {
    toggleAll() {
      const newStatus = !this.areAllFieldsSelected();
      for (const field of this.fields) {
        field.selected = newStatus;
      }
      this.selectAll = newStatus;
    },
    toggleField() {
      this.selectAll = this.areAllFieldsSelected();
    },
    areAllFieldsSelected() {
      console.log(toRaw(this.fields))
      return this.fields.every((field) => field.selected);
    },
    showFields() {
      const selectedFields = this.fields.filter((field) => field.selected);
      console.log(selectedFields, this.selectAll);
    }
  }
}
</script>

<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
