<template>
  <q-page padding>
    <q-card class="text-grey-8">
      <q-card-section class="q-pa-none">
        <q-table
          class="no-shadow"
          :data="data"
          title="Questionari Disponibili"
          :hide-header="mode === 'grid'"
          :columns="columns"
          row-key="name"
          :filter="filter"
          :pagination.sync="pagination"
        >
          <template v-slot:top-right="props">
            <q-input
              borderless
              dense
              class="q-px-md"
              debounce="300"
              v-model="filter"
              placeholder="Cerca"
            >
              <template v-slot:append>
                <q-icon name="search" />
              </template>
            </q-input>

            <q-btn
              color="primary"
              icon-right="archive"
              label="Esporta in csv"
              no-caps
              @click="exportTable"
            />
          </template>
        </q-table>
      </q-card-section>
      <q-card-actions align="right">
        <q-btn
          color="blue-8"
          icon-right="fas fa-plus"
          label="Aggiungi un nuovo questionario"
          to="/questionario"
        />
      </q-card-actions>
    </q-card>
  </q-page>
</template>

<script>
function wrapCsvValue(val, formatFn) {
  let formatted = formatFn !== void 0 ? formatFn(val) : val;

  formatted =
    formatted === void 0 || formatted === null ? "" : String(formatted);

  formatted = formatted.split('"').join('""');
  /**
   * Excel accepts \n and \r in strings, but some other CSV parsers do not
   * Uncomment the next two lines to escape new lines
   */
  // .split('\n').join('\\n')
  // .split('\r').join('\\r')

  return `"${formatted}"`;
}
export default {
  name: "Questionari",

  data() {
    return {
      filter: "",
      mode: "list",
      columns: [
        {
          name: "id",
          align: "left",
          label: "ID Questionario",
          field: "id",
          sortable: true
        },
        /* {
          name: "user_name",
          align: "left",
          label: "User Name",
          field: "user_name",
          sortable: true
        }, */
        {
          name: "response",
          align: "left",
          label: "Risposte",
          field: "response",
          sortable: true
        },
        {
          name: "desc",
          required: true,
          label: "Titolo",
          align: "left",
          field: "desc",
          sortable: true
        },
        {
          name: "date",
          align: "right",
          label: "Data di rilascio",
          field: "date",
          sortable: true
        }
      ],
      data: [
        {
          id: "U0001",
          name: "/login",
          date: "10/01/2021",
          //user_name: "Pratik Patel"
          response: "100",
          desc: "Come vieni a lavoro?"
        },
        {
          id: "U0002",
          name: "/Dashboard",
          date: "13/01/2021",
          //user_name: "Razvan Stoenescu"
          response: "120",
          desc: "Come migliorare la mobilità?"
        },
        {
          id: "U0003",
          name: "/Map",
          date: "10/02/2021",
          //user_name: "Pratik Patel"
          response: "200",
          desc: "Smartworking"
        },
        {
          id: "U0004",
          name: "/Mail",
          date: "13/03/2021",
          //user_name: "Jeff Galbraith"
          response: "220",
          desc: "Hai una bicicletta elettrica?"
        },
        {
          id: "U0005",
          name: "/Profile",
          date: "12/04/2021",
          //user_name: "Pratik Patel"
          response: "220",
          desc: "Car Pooling"
        }
      ],
      pagination: {
        rowsPerPage: 10
      }
    };
  },

  methods: {
    exportTable() {
      // naive encoding to csv format
      const content = [this.columns.map(col => wrapCsvValue(col.label))]
        .concat(
          this.data.map(row =>
            this.columns
              .map(col =>
                wrapCsvValue(
                  typeof col.field === "function"
                    ? col.field(row)
                    : row[col.field === void 0 ? col.name : col.field],
                  col.format
                )
              )
              .join(",")
          )
        )
        .join("\r\n");

      const status = exportFile("table-export.csv", content, "text/csv");

      if (status !== true) {
        this.$q.notify({
          message: "Browser denied file download...",
          color: "negative",
          icon: "warning"
        });
      }
    }
  }
};
</script>

<style></style>
