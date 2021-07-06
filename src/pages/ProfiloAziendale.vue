<template>
  <q-page padding>
    <div class="row q-gutter-md">
      <div class="col-lg-7 col-md-7 col-sm-12 col-xs-12">
        <q-card class="my-card">
          <q-card-section>
            <div class="text-h5 text-bold">
              Informazioni Aziendali
            </div>
          </q-card-section>
          <q-card-section class="column q-gutter-lg">
            <q-input
              v-model="Company.NomeAzienda"
              filled
              type="text"
              label="Ragione Sociale"
            >
              <template v-slot:append>
                <q-btn
                  round
                  flat
                  color="grey-6"
                  size="md"
                  icon="fas fa-times-circle"
                  @click="onClick"
                />
              </template>
            </q-input>

            <div class="row justify-between">
              <q-input
                class="col-5"
                filled
                v-model="Company.PartitaIVA"
                type="text"
                label="Partita IVA"
                mask="AA ###########"
                fill-mask
              >
                <template v-slot:append>
                  <q-btn
                    round
                    flat
                    color="grey-6"
                    size="md"
                    icon="fas fa-times-circle"
                    @click="onClick"
                /></template>
              </q-input>

              <q-input
                class="col-5"
                filled
                v-model="Company.CodiceREA"
                type="text"
                label="Codice REA"
                mask="AA-######"
                fill-mask
              >
                <template v-slot:append>
                  <q-btn
                    round
                    flat
                    color="grey-6"
                    size="md"
                    icon="fas fa-times-circle"
                    @click="onClick"
                  />
                </template>
              </q-input>
            </div>

            <q-select
              v-model="Company.Settore"
              :options="Settori"
              label="Settore"
              filled
            />

            <div class="row justify-between">
              <div class="col-5">
                <q-input
                  filled
                  v-model="Company.Direttore.nome"
                  type="text"
                  label="Nome Direttore"
                />
              </div>

              <div class="col-5">
                <q-input
                  filled
                  v-model="Company.Direttore.cognome"
                  type="text"
                  label="Cognome Direttore"
                />
              </div>
            </div>

            <div class="row justify-between">
              <div class="col-5">
                <q-input
                  filled
                  v-model="Company.MobilityManager.nome"
                  type="text"
                  label="Nome Responsabile Mobilità"
                />
              </div>

              <div class="col-5">
                <q-input
                  filled
                  v-model="Company.MobilityManager.cognome"
                  type="text"
                  label="Cognome Responsabile Mobilità"
                />
              </div>
            </div>
          </q-card-section>
        </q-card>

        <q-card class="my-card q-mt-md">
          <q-card-section>
            <div class="text-h5 text-bold">
              Numero e Tipologia dei Dipendenti
            </div>
          </q-card-section>
          <q-card-section>
            <div class="text-bold text-h8 q-mb-sm">
              Numero totale di dipendenti nel luogo di lavoro indicato:
            </div>
            <div class="row justify-between q-gutter-sm">
              <div class="col-2">
                <q-input
                  filled
                  v-model="Company.Dipendenti.totale"
                  type="number"
                >
                  <template v-slot:before>
                    <div
                      class="text-grey-9 ellipsis-2-lines"
                      style="font-size: 14px; max-width: 200px"
                    >
                      Totale:
                    </div>
                  </template>
                </q-input>
              </div>

              <div class="col-2">
                <q-input
                  filled
                  v-model="Company.Dipendenti.fullTime"
                  type="number"
                >
                  <template v-slot:before>
                    <div
                      class="text-grey-9 ellipsis-2-lines"
                      style="font-size: 14px; max-width: 200px"
                    >
                      Full-Time:
                    </div>
                  </template>
                </q-input>
              </div>

              <div class="col-2">
                <q-input
                  filled
                  v-model="Company.Dipendenti.partTime"
                  type="number"
                >
                  <template v-slot:before>
                    <div
                      class="text-grey-9 ellipsis-2-lines"
                      style="font-size: 14px; max-width: 200px"
                    >
                      Part-Time:
                    </div>
                  </template>
                </q-input>
              </div>

              <div class="col-2">
                <q-input
                  filled
                  v-model="Company.Dipendenti.turnisti"
                  type="number"
                >
                  <template v-slot:before>
                    <div
                      class="text-grey-9 ellipsis-2-lines"
                      style="font-size: 14px; max-width: 200px"
                    >
                      Turnisti:
                    </div>
                  </template>
                </q-input>
              </div>
            </div>
          </q-card-section>
          <q-card-section>
            <div class="text-h5 text-bold">
              Orario Attività
            </div>
            <div class="text-bold q-mb-sm">
              Quale è l'orario di attività?
            </div>
            <div class="row justify-center q-gutter-lg">
              <div class="col-3">
                <q-input
                  v-model="Company.OrarioAttivita.inizio"
                  filled
                  mask="time"
                  fill-mask
                  :rules="['time']"
                  hint="Orario di Inizio"
                >
                  <template v-slot:append>
                    <q-icon name="far fa-clock" />
                  </template>
                </q-input>
              </div>

              <div class="col-3">
                <q-input
                  v-model="Company.OrarioAttivita.fine"
                  filled
                  mask="time"
                  fill-mask
                  :rules="['time']"
                  hint="Orario di Fine"
                >
                  <template v-slot:append>
                    <q-icon name="far fa-clock" />
                  </template>
                </q-input>
              </div>
            </div>

            <div class="text-bold text-h8 q-my-sm">
              L'attività prevede l'uso di turni?
            </div>
            <div>
              <q-toggle
                v-model="Company.isTurni"
                color="blue-8"
                label="Sì, prevede l'uso di turni"
              />
            </div>

            <div class="q-mt-md" v-if="Company.isTurni">
              <div
                class="row justify-center q-gutter-md q-mb-sm"
                v-for="(time, index) in Company.Turni"
                :key="index"
              >
                <div class="col-2">
                  <q-input
                    :v-model="time.Orario.inizio"
                    filled
                    mask="time"
                    fill-mask
                    :rules="['time']"
                    hint="Orario di Inizio"
                  >
                    <template v-slot:append>
                      <q-icon name="far fa-clock" />
                    </template>
                  </q-input>
                </div>
                <div class="col-2">
                  <q-input
                    :v-model="time.Orario.fine"
                    filled
                    mask="time"
                    fill-mask
                    :rules="['time']"
                    hint="Orario di Fine"
                  >
                    <template v-slot:append>
                      <q-icon name="far fa-clock" />
                    </template>
                  </q-input>
                </div>

                <div class="col-2">
                  <q-input
                    v-model="time.turnisti"
                    filled
                    type="number"
                    label="N° Turnisti"
                  />
                </div>
              </div>
            </div>
            <div class="row q-gutter-md q-mt-sm">
              <div class="text-h5 text-bold q-my-md">
                É presente una mensa aziendale?
              </div>
              <div>
                <q-toggle
                  v-model="Company.isMensa"
                  color="blue-8"
                  label="Sì, la mia attività ha una mensa"
                />
              </div>
            </div>
          </q-card-section>
        </q-card>
      </div>
      <!-- BARRA LATERALE -->
      <div class="col-lg-4 col-md-4 col-sm-12 col-xs-12">
        <q-card class="my-card">
          <q-card-section class="">
            <div class="text-h6 text-bold text-left">
              Logo Aziendale
            </div>
            <div class="flex flex-center q-mt-sm">
              <q-uploader
                url="http://localhost:4444/upload"
                color="blue-8"
                flat
                bordered
                style="max-width: 800px"
              />
            </div>
          </q-card-section>
          <q-card-section>
            <div class="text-h6 text-bold q-mb-sm">
              Informazioni Generali
            </div>
            <div class="row justify-between">
              <div class="col-8">
                <q-input
                  filled
                  v-model="Company.Citta"
                  type="text"
                  label="Città"
                />
              </div>
              <div class="col-3">
                <q-input
                  filled
                  v-model="Company.CAP"
                  type="number"
                  label="CAP"
                />
              </div>
            </div>

            <div class="row justify-between q-mt-md">
              <div class="col-8">
                <q-input filled v-model="Company.Via" type="text" label="Via" />
              </div>
              <div class="col-3">
                <q-input
                  filled
                  v-model="Company.Numero"
                  type="number"
                  label="N°"
                />
              </div>
            </div>
          </q-card-section>
          <q-card-section>
            <div class="text-h6 text-bold q-mb-sm">
              Informazioni di Contatto
            </div>

            <div class="row justify-between q-mb-md">
              <div class="col-5">
                <q-input
                  filled
                  v-model="Company.Telefono"
                  type="text"
                  label="Numero di Telefono"
                  mask="(+39) ##########"
                  fill-mask
                />
              </div>

              <div class="col-5">
                <q-input
                  filled
                  v-model="Company.Fax"
                  type="text"
                  label="Fax"
                  mask="(+39) ##########"
                  fill-mask
                />
              </div>
            </div>

            <q-input
              filled
              v-model="Company.Email"
              type="text"
              label="Indirizzo Email"
            />
          </q-card-section>
        </q-card>
      </div>
    </div>
  </q-page>
</template>

<script>
export default {
  data() {
    return {
      Company: {
        NomeAzienda: "",
        PartitaIVA: "",
        CodiceREA: "",
        Settore: "",
        Citta: "",
        Via: "",
        Numero: "",
        CAP: "",
        Telefono: "",
        Fax: "",
        Email: "",
        Direttore: {
          nome: "",
          cognome: ""
        },
        MobilityManager: {
          nome: "",
          cognome: ""
        },
        Dipendenti: {
          totale: "",
          fullTime: "",
          partTime: "",
          turnisti: ""
        },
        OrarioAttivita: {
          inizio: "",
          fine: ""
        },
        isTurni: false,
        Turni: [
          {
            Orario: {
              inizio: "",
              fine: ""
            },
            turnisti: ""
          },
          {
            Orario: {
              inizio: "",
              fine: ""
            },
            turnisti: ""
          },
          {
            Orario: {
              inizio: "",
              fine: ""
            },
            turnisti: ""
          },
          {
            Orario: {
              inizio: "",
              fine: ""
            },
            turnisti: ""
          }
        ],
        isMensa: false
      },
      Settori: ["Immobiliare", "Ente Pubblico", "Industriale", "Commerciale"]
    };
  }
};
</script>

<style></style>
