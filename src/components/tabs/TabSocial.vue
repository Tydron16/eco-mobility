<template>
  <div class="col-lg-6 col-md-6 col-sm-12 col-xs-12">
    <q-card class="fit">
      <q-card-section>
        <div class="text-h6 text-bold text-grey-9">
          Elenco Dipendenti
        </div>
      </q-card-section>
      <q-card-section>
        <q-list class="rounded-borders" separator>
          <q-item
            v-for="(contact, index) in contacts"
            :key="index"
            clickable
            v-ripple
          >
            <q-item-section avatar>
              <q-avatar>
                <img :src="contact.avatar" />
              </q-avatar>
            </q-item-section>

            <q-item-section>
              <q-item-label lines="1">{{ contact.name }}</q-item-label>
              <q-item-label caption lines="2">
                <span class="text-weight-bold">{{ contact.position }}</span>
              </q-item-label>
            </q-item-section>

            <q-item-section side>
              <div class="text-grey-8 q-gutter-xs">
                <q-btn
                  class="gt-xs"
                  size="md"
                  flat
                  color="blue"
                  dense
                  round
                  icon="comment"
                />
                <q-btn
                  class="gt-xs"
                  size="md"
                  flat
                  color="red"
                  dense
                  round
                  icon="email"
                />
                <q-btn size="md" flat dense round color="green" icon="phone" />
              </div>
            </q-item-section>
          </q-item>
        </q-list>
      </q-card-section>
      <q-card-actions align="right">
        <q-btn
          color="blue-8"
          icon-right="chevron_right"
          label="Vedi l'elenco completo"
        />
      </q-card-actions>
    </q-card>
  </div>
</template>

<script>
export default {
  name: "TabSocial",
  data() {
    return {
      tab: "contact",
      contacts: [
        {
          name: "Claudio Pacini",
          position: "Professionista",
          avatar: "https://avatars2.githubusercontent.com/u/34883558?s=400&v=4"
        },
        {
          name: "Giuseppe Gallinari",
          position: "Operaio",
          avatar: "https://cdn.quasar.dev/team/razvan_stoenescu.jpeg"
        },
        {
          name: "Sirio Belli",
          position: "Manager",
          avatar: "https://cdn.quasar.dev/team/jeff_galbraith.jpg"
        },
        {
          name: "Anna Rossi",
          position: "Impiegata",
          avatar: "https://cdn.quasar.dev/img/avatar2.jpg"
        },
        {
          name: "Maria Santi",
          position: "Marketing Manager",
          avatar: "https://cdn.quasar.dev/img/avatar6.jpg"
        }
      ]
    };
  }
};
</script>
