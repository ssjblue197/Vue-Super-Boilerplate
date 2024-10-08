<template>
  <div class="wrapper">
    <div class="relative mx-auto mt-8 w-[90%]">
      <p-calendar
        class="mb-8"
        :value="local.date"
        type="multiple"
        ref="calendar"
        format="DD-MM-YYYY"
        @p-change="handleChangeDate"
      ></p-calendar>
      <p-table
        :options="local.options"
        :loading="local.loading"
        :data="local.items"
      ></p-table>
    </div>
  </div>
</template>

<script setup lang="ts">
import { html } from 'lit';
import { reactive, onMounted, ref } from 'vue';
import formatter from 'pure-date-format';
interface RowData {
  name: string;
  age: string;
  address: {
    street: string;
    department: string;
    city: string;
    country: string;
  };
  status: number;
}

interface Local {
  options: any;
  keyword: string;
  date: (string | Date)[];
  loading: boolean;
  items: RowData[];
}

const calendar = ref(null);

const local: Local = reactive({
  options: {
    paginate: true,
    columns: [
      {
        field: 'name',
        id: 'name',
        headerName: 'Full name',
        minWidth: '120px',
        alignItems: 'center',
        justifyContent: 'flex-start',
      },
      { field: 'age', id: 'age', headerName: 'Age' },
      {
        field: 'address.street',
        id: 'street',
        headerName: 'Street',
      },
      {
        field: 'address.department',
        id: 'department',
        headerName: 'Department',
      },
      {
        field: 'address.city',
        id: 'city',
        headerName: 'City',
      },
      {
        field: 'address.country',
        id: 'country',
        headerName: 'Country',
      },
      {
        field: 'status',
        id: 'status',
        headerName: 'Status',
        render: (row: RowData) =>
          html`<p-tag
            variant="${row.status ? 'success' : 'danger'}"
            size="small"
            >${row.status ? 'Active' : 'Inactive'}</p-tag
          >`,
      },
      {
        field: '',
        id: 'action',
        headerName: 'Action',
        render: (row: RowData) => {
          return html`<p-button
            outline
            variant="primary"
            size="small"
            >Support</p-button
          >`;
        },
      },
    ],
  },
  keyword: '',
  date: ['06-09-2024', '07-09-2024', new Date()],
  loading: false,
  items: [],
});

const fetchData = async () => {
  try {
    local.loading = true;
    const promise = new Promise((resolve) => {
      setTimeout(() => {
        resolve([
          {
            name: 'Alice',
            age: '28',
            address: {
              street: '2 Elm Street',
              department: 'Greenwood',
              city: 'Portland',
              country: 'USA',
            },
            status: 1,
          },
          {
            name: 'Bob',
            age: '35',
            address: {
              street: '3 Oak Street',
              department: 'Lakeside',
              city: 'Chicago',
              country: 'USA',
            },
            status: 0,
          },
          {
            name: 'Charlie',
            age: '22',
            address: {
              street: '4 Pine Street',
              department: 'Downtown',
              city: 'San Francisco',
              country: 'USA',
            },
            status: 1,
          },
          {
            name: 'David',
            age: '40',
            address: {
              street: '5 Maple Street',
              department: 'Westside',
              city: 'Los Angeles',
              country: 'USA',
            },
            status: 0,
          },
          {
            name: 'Eva',
            age: '31',
            address: {
              street: '6 Birch Street',
              department: 'Riverside',
              city: 'Austin',
              country: 'USA',
            },
            status: 1,
          },
          {
            name: 'Frank',
            age: '29',
            address: {
              street: '7 Cedar Street',
              department: 'Northside',
              city: 'Denver',
              country: 'USA',
            },
            status: 0,
          },
          {
            name: 'Grace',
            age: '33',
            address: {
              street: '8 Willow Street',
              department: 'Southside',
              city: 'Miami',
              country: 'USA',
            },
            status: 1,
          },
          {
            name: 'Hannah',
            age: '25',
            address: {
              street: '9 Walnut Street',
              department: 'Eastside',
              city: 'Boston',
              country: 'USA',
            },
            status: 0,
          },
          {
            name: 'Ivy',
            age: '27',
            address: {
              street: '10 Chestnut Street',
              department: 'Central',
              city: 'Philadelphia',
              country: 'USA',
            },
            status: 1,
          },
          {
            name: 'Jack',
            age: '32',
            address: {
              street: '11 Ash Street',
              department: 'Uptown',
              city: 'Atlanta',
              country: 'USA',
            },
            status: 0,
          },
          {
            name: 'Karen',
            age: '36',
            address: {
              street: '12 Fir Street',
              department: 'Midtown',
              city: 'Seattle',
              country: 'USA',
            },
            status: 1,
          },
          {
            name: 'Leo',
            age: '24',
            address: {
              street: '13 Poplar Street',
              department: 'Parkside',
              city: 'San Diego',
              country: 'USA',
            },
            status: 0,
          },
          {
            name: 'Mia',
            age: '26',
            address: {
              street: '14 Sycamore Street',
              department: 'Harbor',
              city: 'San Jose',
              country: 'USA',
            },
            status: 1,
          },
          {
            name: 'Nina',
            age: '29',
            address: {
              street: '15 Magnolia Street',
              department: 'Hilltop',
              city: 'Las Vegas',
              country: 'USA',
            },
            status: 0,
          },
          {
            name: 'Oliver',
            age: '31',
            address: {
              street: '16 Hickory Street',
              department: 'Downtown',
              city: 'Orlando',
              country: 'USA',
            },
            status: 1,
          },
          {
            name: 'Paula',
            age: '37',
            address: {
              street: '17 Locust Street',
              department: 'Sunset',
              city: 'Honolulu',
              country: 'USA',
            },
            status: 0,
          },
          {
            name: 'Quinn',
            age: '23',
            address: {
              street: '18 Elm Street',
              department: 'Springfield',
              city: 'New York',
              country: 'USA',
            },
            status: 1,
          },
          {
            name: 'Rachel',
            age: '34',
            address: {
              street: '19 Redwood Street',
              department: 'Elmwood',
              city: 'Washington',
              country: 'USA',
            },
            status: 0,
          },
          {
            name: 'Steve',
            age: '38',
            address: {
              street: '20 Oak Street',
              department: 'Creekside',
              city: 'Dallas',
              country: 'USA',
            },
            status: 1,
          },
        ]);
      }, 2000);
    });
    const data = await promise;
    local.items = data as RowData[];
  } catch (error) {
  } finally {
    local.loading = false;
  }
};

const handleChangeDate = (e: Event) => {
  console.log('e', e);
};
onMounted(() => {
  fetchData();
  const valid = formatter().isValid(
    '08-10-1997 +02:00',
    'DD-MM-YYYY Z',
  );
  console.log('valid', valid);
});
</script>

<style scoped></style>
