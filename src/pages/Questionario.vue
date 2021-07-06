<template>
  <q-page padding>
    <div class="text-h4 text-bold q-mb-md">
      Compila un nuovo questionario
    </div>
    <div class="row q-gutter-md">
      <div class="col-lg-7 col-md-7 col-sm-12 col-xs-12">
        <q-card class="my-card">
          <q-card-section>
            <div class="text-h5 text-bold">Orario di lavoro</div>
          </q-card-section>
          <q-card-section>
            <div class="row">
              <div class="text-bold text-h7 col-md-4 col-sm-8">
                Che tipo di contratto hai?
              </div>
              <div class="col-4">
                <q-option-group
                  v-model="Dipendenti.Contratto"
                  type="radio"
                  inline
                  color="blue-8"
                  :options="tipologiaContratto"
                />
              </div>
            </div>
          </q-card-section>
          <q-card-section>
            <div class="row">
              <div class="text-h7 text-bold self-center col-md-2 col-sm-8">
                Sei un turnista?
              </div>
              <div class="col-md-3 col-sm-8">
                <q-toggle
                  v-model="Dipendenti.isTurnisti"
                  color="blue-8"
                  label="Sì, sono un turnista."
                />
              </div>
            </div>
          </q-card-section>
          <q-card-section v-if="!Dipendenti.isTurnisti">
            <div class="row">
              <div class="col-md-5 col-sm-8">
                <div class="text-bold text-h7 q-mb-md">
                  Quali sono di norma i tuoi orari di inizio e fine lavoro?
                </div>
                <div class="text-body2 q-mx-sm">
                  Compila solo la <strong>mattina</strong> della tabella se
                  <strong>non</strong> rientri a casa durante la giornata
                  lavorativa. Se rientri, invece, indica gli orari relativi alla
                  sola mattina. <br /><br />
                  Compila l'orario <strong>promeridiano</strong> della tabella
                  indicando gli orari lavorativi dopo il rientro da casa.
                </div>
              </div>

              <div class="col-7">
                <q-table
                  flat
                  bordered
                  title="Tabella oraria"
                  :data="rows"
                  :columns="columns"
                  row-key="name"
                >
                  <template v-slot:body="props">
                    <q-tr :props="props">
                      <q-td
                        key="orario"
                        :props="props"
                        :class="props.rowIndex > 1 ? 'bg-grey-3' : ''"
                      >
                        {{ props.row.name }}
                        <div
                          class="text-caption text-grey-7"
                          v-if="props.rowIndex > 1"
                        >
                          (pomeridiano)
                        </div>
                        <div class="text-caption text-grey-7" v-else>
                          (mattina)
                        </div>
                      </q-td>
                      <q-td
                        key="lun"
                        :props="props"
                        :class="props.rowIndex > 1 ? 'bg-grey-3' : ''"
                      >
                        <div v-if="!props.row.lun">
                          <q-icon name="fas fa-pen" />
                        </div>
                        {{ props.row.lun }}
                        <q-popup-edit
                          v-model="props.row.lun"
                          title="Modifica l'orario"
                        >
                          <q-input
                            v-model="props.row.lun"
                            autofocus
                            dense
                            mask="time"
                            fill-mask
                            :rules="['time']"
                          >
                            <template v-slot:append>
                              <q-icon name="far fa-clock" />
                            </template>
                          </q-input>
                        </q-popup-edit>
                      </q-td>

                      <q-td
                        key="mar"
                        :props="props"
                        :class="props.rowIndex > 1 ? 'bg-grey-3' : ''"
                      >
                        <div v-if="!props.row.mar">
                          <q-icon name="fas fa-pen" />
                        </div>
                        {{ props.row.mar }}
                        <q-popup-edit
                          v-model="props.row.mar"
                          title="Modifica l'orario"
                        >
                          <q-input
                            v-model="props.row.mar"
                            autofocus
                            dense
                            mask="time"
                            fill-mask
                            :rules="['time']"
                          >
                            <template v-slot:append>
                              <q-icon name="far fa-clock" />
                            </template>
                          </q-input>
                        </q-popup-edit>
                      </q-td>
                      <q-td
                        key="mer"
                        :props="props"
                        :class="props.rowIndex > 1 ? 'bg-grey-3' : ''"
                      >
                        <div v-if="!props.row.mer">
                          <q-icon name="fas fa-pen" />
                        </div>
                        {{ props.row.mer }}
                        <q-popup-edit
                          v-model="props.row.mer"
                          title="Modifica l'orario"
                        >
                          <q-input
                            v-model="props.row.mer"
                            autofocus
                            dense
                            mask="time"
                            fill-mask
                            :rules="['time']"
                          >
                            <template v-slot:append>
                              <q-icon name="far fa-clock" />
                            </template>
                          </q-input>
                        </q-popup-edit>
                      </q-td>
                      <q-td
                        key="gio"
                        :props="props"
                        :class="props.rowIndex > 1 ? 'bg-grey-3' : ''"
                      >
                        <div v-if="!props.row.gio">
                          <q-icon name="fas fa-pen" />
                        </div>
                        {{ props.row.gio }}
                        <q-popup-edit
                          v-model="props.row.gio"
                          title="Modifica l'orario"
                        >
                          <q-input
                            v-model="props.row.gio"
                            autofocus
                            dense
                            mask="time"
                            fill-mask
                            :rules="['time']"
                          >
                            <template v-slot:append>
                              <q-icon name="far fa-clock" />
                            </template>
                          </q-input>
                        </q-popup-edit>
                      </q-td>
                      <q-td
                        key="ven"
                        :props="props"
                        :class="props.rowIndex > 1 ? 'bg-grey-3' : ''"
                      >
                        <div v-if="!props.row.ven">
                          <q-icon name="fas fa-pen" />
                        </div>
                        {{ props.row.ven }}
                        <q-popup-edit
                          v-model="props.row.ven"
                          title="Modifica l'orario"
                        >
                          <q-input
                            v-model="props.row.ven"
                            autofocus
                            dense
                            mask="time"
                            fill-mask
                            :rules="['time']"
                          >
                            <template v-slot:append>
                              <q-icon name="far fa-clock" />
                            </template>
                          </q-input>
                        </q-popup-edit>
                      </q-td>
                      <q-td
                        key="sab"
                        :props="props"
                        :class="props.rowIndex > 1 ? 'bg-grey-3' : ''"
                      >
                        <div v-if="!props.row.sab">
                          <q-icon name="fas fa-pen" />
                        </div>
                        {{ props.row.sab }}
                        <q-popup-edit
                          v-model="props.row.sab"
                          title="Modifica l'orario"
                        >
                          <q-input
                            v-model="props.row.sab"
                            autofocus
                            dense
                            mask="time"
                            fill-mask
                            :rules="['time']"
                          >
                            <template v-slot:append>
                              <q-icon name="far fa-clock" />
                            </template>
                          </q-input>
                        </q-popup-edit>
                      </q-td>
                      <q-td
                        key="dom"
                        :props="props"
                        :class="props.rowIndex > 1 ? 'bg-grey-3' : ''"
                      >
                        <div v-if="!props.row.dom">
                          <q-icon name="fas fa-pen" />
                        </div>
                        {{ props.row.dom }}
                        <q-popup-edit
                          v-model="props.row.dom"
                          title="Modifica l'orario"
                        >
                          <q-input
                            v-model="props.row.dom"
                            autofocus
                            dense
                            mask="time"
                            fill-mask
                            :rules="['time']"
                          >
                            <template v-slot:append>
                              <q-icon name="far fa-clock" />
                            </template>
                          </q-input>
                        </q-popup-edit>
                      </q-td>
                    </q-tr>
                  </template>
                </q-table>
              </div>
            </div>
          </q-card-section>
          <q-card-section v-else> </q-card-section>
        </q-card>
      </div>
      <!-- BARRA LATERALE -->
      <div class="col-lg-4 col-md-4 col-sm-12 col-xs-12">
        <q-card class="my-card">
          <q-card-section>
            <div class="text-h6 text-bold">Pubblicazione</div>
          </q-card-section>
          <q-card-section>
            <div class="row justify-between">
              <div
                class="col-6 self-center text-bold text-h7 text-grey-7"
                style="font-size: 16px"
              >
                Stato
              </div>
              <div class="col-4">
                <q-chip
                  class="text-white text-bold"
                  color="green-4"
                  label="Pubblicato"
                />
              </div>
            </div>
            <div class="row justify-between q-mt-md">
              <div
                class="col-6 self-center text-bold text-h7 text-grey-7"
                style="font-size: 16px"
              >
                Ultimo aggiornamento
              </div>
              <div class="col-3 text-bold text-grey-9">
                1h fa
              </div>
            </div>
          </q-card-section>
          <q-card-actions align="right">
            <q-btn color="blue-8" label="Aggiorna" />
          </q-card-actions>
        </q-card>
        <q-card class="q-mt-md">
          <q-card-section>
            <div class="text-h6 text-bold">Divulgazione</div>
          </q-card-section>
          <q-card-section>
            <q-input
              v-model="generatedURL"
              :loading="loadingState"
              type="text"
              readonly
              label="URL da condividere"
            >
              <template v-slot:after>
                <q-btn
                  flat
                  color="grey-5"
                  icon="far fa-copy"
                  @click="copyURL()"
                />
              </template>
            </q-input>
            <div class="text-negative text-caption" v-if="isError">
              Errore sconosciuto
            </div>
          </q-card-section>
          <q-card-actions align="right">
            <q-btn color="blue-8" label="Genera URL" @click="generateURL()" />
          </q-card-actions>
        </q-card>
      </div>
    </div>
  </q-page>
</template>

<script>
const columns = [
  {
    name: "orario",
    label: "Orario",
    align: "center",
    field: row => row.name,
    format: val => `${val}`
  },
  {
    name: "lun",
    label: "Lunedì",
    align: "center",
    field: "lun"
  },
  {
    name: "mar",
    field: "mar",
    label: "Martedì",
    align: "center"
  },
  {
    name: "mer",
    field: "mer",
    label: "Mercoledì",
    align: "center"
  },
  {
    name: "gio",
    field: "gio",
    label: "Giovedì",
    align: "center"
  },
  {
    name: "ven",
    field: "ven",
    label: "Venerdì",
    align: "center"
  },
  {
    name: "sab",
    field: "sab",
    label: "Sabato",
    align: "center"
  },
  {
    name: "dom",
    field: "dom",
    label: "Domenica",
    align: "center"
  }
];

const rows = [
  {
    name: "Inizio",
    lun: "",
    mar: "",
    mer: "",
    gio: "",
    ven: "",
    sab: "",
    dom: ""
  },
  {
    name: "Fine",
    lun: "",
    mar: "",
    mer: "",
    gio: "",
    ven: "",
    sab: "",
    dom: ""
  },
  {
    name: "Inizio",
    lun: "",
    mar: "",
    mer: "",
    gio: "",
    ven: "",
    sab: "",
    dom: ""
  },
  {
    name: "Fine",
    lun: "",
    mar: "",
    mer: "",
    gio: "",
    ven: "",
    sab: "",
    dom: ""
  }
];

export default {
  mixins: {
    receivedData(data) {
      this.loadingState = false;
      this.generatedURL = data.link;
    }
  },
  data() {
    return {
      columns,
      rows,
      Dipendenti: {
        Contratto: "",
        isTurnisti: false
      },

      tipologiaContratto: [
        {
          label: "Part-time",
          value: "part-time"
        },
        {
          label: "Full-time",
          value: "full-time"
        },
        {
          label: "A turnazione",
          value: "turnazione"
        },
        {
          label: "Orario flessibile",
          value: "flessibile"
        },
        {
          label: "Orario fisso",
          value: "fisso"
        }
      ],
      generatedURL: "",
      loadingState: false,
      bitLyAPIKey: "c961e3914fd9674b62b2ad27086a7ed0d288edb4",
      bitLyAPIURL: "https://api-ssl.bitly.com/v4/shorten",
      bitLyBaseURL: "https://api-ssl.bitly.com",
      isError: false
    };
  },

  methods: {
    copyURL() {},

    generateURL() {
      this.loadingState = true;

      const config = {
        headers: {
          Authorization: `Bearer c961e3914fd9674b62b2ad27086a7ed0d288edb4`,
          "Content-Type": "application/json"
        }
      };

      const bodyParameters = {
        long_url: "https://capacitag.com/"
      };

      this.$axios
        .post(this.bitLyAPIURL, bodyParameters, config)
        .then(response => (this.generatedURL = response.data.link))
        .catch(() => (this.isError = true))
        .then((this.loadingState = false));
    }
  }
};
</script>

<style></style>
