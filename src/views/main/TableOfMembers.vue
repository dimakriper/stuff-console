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
        :sort-by.sync="sortBy"
        :sort-desc.sync="sortDesc"
        sort-icon-left
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
          <message-form @hide-details="row.toggleDetails" v-if="row.item.selectedAction.key === 'message'"></message-form>
          <payout-form @hide-details="row.toggleDetails" v-else-if="row.item.selectedAction.key === 'pay_out'"></payout-form>
        </b-card>
      </template>

      <template #cell(last_login)="row">
        {{ formatDate(row.item.last_login) }}
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
import MessageForm from "@/views/main/MessageForm.vue";
import PayoutForm from "@/views/main/PayoutForm.vue";

let members = require('@/assets/members.json');
members.forEach(mem => {mem.selectedAction = {key: "pay_out", label: "Payout"}})
export default {
  components: {PayoutForm, MessageForm},
  data() {
    return {
      sortBy: 'last_login',
      sortDesc: true,
      perPage: 5,
      currentPage: 1,
      items: members,
      fields: [
        {key: 'name', label: 'Name', },
        {key: 'age', label: 'Age', sortable: true},
        {key: 'last_login', label: 'Last login', sortable: true},
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
    formatDate(unix_date){
      let date = new Date(unix_date);
      return date.toLocaleString()
    },
    selectAction(row, item){
      row.item.selectedAction = item;
      if (!row.detailsShowing) row.toggleDetails();
    }
  }
}
</script>

<style scoped>

</style>