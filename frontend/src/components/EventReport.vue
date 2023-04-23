<template>
  <div class="center">
    <vs-table class="report-table">
      <template #thead >
        <vs-tr>
          <vs-th>Event ID</vs-th>
          <vs-th>Name</vs-th>
          <vs-th>Organizer</vs-th>
          <vs-th>Date</vs-th>
          <vs-th>Ticket type</vs-th>
          <vs-th>Rs. from Normal</vs-th>
          <vs-th>Rs. from Silver</vs-th>
          <vs-th>Rs. from Gold</vs-th>
          <vs-th>Rs. from Platinum</vs-th>
          <vs-th>Total revenue</vs-th>
        </vs-tr>
      </template>
      <template #tbody>
        <vs-tr :key="i" v-for="(tr, i) in report_data" :data="tr">
          <vs-td>#{{ tr.event_id }}</vs-td>
          <vs-td>{{ tr.e_name }}</vs-td>
          <vs-td>{{ tr.e_organizer }}</vs-td>
          <vs-td>{{ tr.e_date }}</vs-td>
          <vs-td v-if="tr.t_type == 0">Normal</vs-td>
          <vs-td v-if="tr.t_type == 1">Premium</vs-td>
          <vs-td>Rs.{{ tr.n_rev }}</vs-td>
          <vs-td>Rs.{{ tr.s_rev }}</vs-td>
          <vs-td>Rs.{{ tr.g_rev }}</vs-td>
          <vs-td>Rs.{{ tr.p_rev }}</vs-td>
          <vs-td>Rs.{{ tr.total_revenue }}</vs-td>
        </vs-tr>
      </template>
    </vs-table>
  </div>
</template>

<script>
import axios from '../vuexios';

export default {
  data() {
    return {
      report_data: [],
    };
  },
  mounted() {
    axios
      .get('/getsalesdetails')
      .then(response => {
        this.report_data = response.data;
      })
      .catch(error => console.log(error.message));
  },
  name: 'EventReport',
};
</script>

<style scoped>
.report-table {
  height: relative !important;
  max-height: 500px;
  overflow: hidden;
  background-color: #D8D4F2;
}

</style>
