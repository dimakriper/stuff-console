<template>

  <div >
    <b-table
        style="text-align: left"
        striped responsive="sm"
        id="my-table"
        :items="items"
        :fields="fields"
        :per-page="perPage"
        :current-page="currentPage"
        small
    >
      <template #cell(show_details)="row">
        <b-dropdown @click="selectAction(row, row.item.selectedAction)"
                    split id="dropdown-dropright"
                    dropright
                    :text="row.item.selectedAction.label"
                    variant="success"
                    class="sm-2"
                    size="sm"
        >
          <b-dropdown-item v-for="(item) in actions" @click="selectAction(row, item)">{{item.label}}</b-dropdown-item>
        </b-dropdown>
      </template>

      <template #row-details="row">
        <b-card>
          <b-row class="mb-2">
            <b-col sm="3" class="text-sm-right"><b>Age:</b></b-col>
            <b-col>{{ row.item.age }}</b-col>
          </b-row>

          <b-button size="sm"  @click="row.toggleDetails">Cancel</b-button>
          <b-button size="sm" variant="danger" @click="row.toggleDetails">Submit</b-button>
        </b-card>
      </template>
    </b-table>
    <div class="col">
      <b-pagination
          v-model="currentPage"
          :total-rows="rows"
          :per-page="perPage"
          aria-controls="my-table"
      ></b-pagination>
    </div>
  </div>
</template>

<script>
let members = require('@/assets/members.json');
members.forEach(mem => {mem.selectedAction = {key: "pay_out", label: "Payout"}})
export default {
  data() {
    return {
      perPage: 5,
      currentPage: 1,
      items: members,
      fields: [
        {key: 'name', label: 'Name', },
        {key: 'age', label: 'Age', },
        {key: 'last_login', label: 'Last login', },
        {key: 'show_details', label: '', },
      ],
      actions: [
        {key: 'pay_out', label: 'Payout', },
        {key: 'message', label: 'Message', },
      ]
    }
  },
  computed: {
    rows() {
      return this.items.length
    }
  },
  methods: {
    selectAction(row, item){
      row.item.selectedAction = item;
      if (!row.detailsShowing) row.toggleDetails();
    }
  }
}
</script>

<style scoped>

</style>