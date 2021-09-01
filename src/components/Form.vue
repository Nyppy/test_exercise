<template>
  <form class="form" @submit.prevent="submit">

    <v-select
      :items="country"
      v-model="locale"
      :label="translate_locale[locale]"
      class="mb-4"
    ></v-select>

    <div
      v-for="i in listFields[locale]"
      :key="i.id"
      class="d-flex flex-column mb-4"
    >
      <v-text-field
        v-model="data_form[i.name]"
        :label="i.label"
        :required="i.required"
        hide-details
        :name="i.name"
        type="text"
        v-maska="i.mask"
      ></v-text-field>

      <span v-if="i.desc" class="mt-2 text-left text-caption">* {{i.desc}}</span>
    </div>
  </form>
</template>

<script>
import Vue from 'vue'

import Maska from 'maska';
Vue.use(Maska);

export default {
  name: 'Form',
  data() {
    return {
      data_form: {},

      locale: 'ru',

      translate_locale: {
        ru: 'Страна',
        gb: 'Сountry',
        de: 'Land',
      },

      country: [
        {
          text: 'Россия',
          value: 'ru'
        },
        {
          text: 'United Kingdom',
          value: 'gb'
        },
        {
          text: 'Deutschland',
          value: 'de'
        },
      ]
    }
  },
  computed: {
    listFields() {
      return {
        ru: [
          {
            name: 'street',
            placeholder: 'Улица, номер дома, номер квартиры',
            label: 'Название улицы, номер дома, номер квартиры',
            desc: 'Название улицы номер дома и номер квартиры вводите через запятую',
            required: false,
          },
          {
            name: 'city',
            placeholder: 'Город',
            label: 'Название населенного пункта (города, поселка и т.п.)',
            desc: null,
            required: true,
          },
          {
            name: 'region',
            placeholder: 'Область',
            label: 'Название республики, края, области, автономного округа',
            desc: null,
            required: true,
          },
          {
            name: 'country',
            placeholder: 'Название страны',
            label: 'Название страны',
            desc: null,
            required: true,
          },
          {
            name: 'index',
            placeholder: 'Индекс',
            label: 'Индекс',
            desc: null,
            required: true,
            mask: '### ###',
          },
        ],
        gb: [
          {
            name: 'street',
            placeholder: 'House number, street name, additional data',
            label: 'House number, street name, addition (for example, which apartment)',
            desc: 'Enter the house number, street name and additional data separated by commas',
            required: false,
          },
          {
            name: 'city',
            placeholder: 'Name of the settlement',
            label: 'Name of the settlement',
            desc: null,
            required: true,
          },
          {
            name: 'index',
            placeholder: 'Postcode',
            label: 'Postcode',
            desc: null,
            required: true,
            mask: 'SS#S #SS',
          },
          {
            name: 'country',
            placeholder: 'The name of the country',
            label: 'The name of the country',
            desc: null,
            required: true,
          },
        ],
        de: [
          {
            name: 'street',
            placeholder: 'Straßenname, Hausnummer',
            label: 'Straßenname, Hausnummer',
            desc: 'Geben Sie den Straßennamen und die Hausnummer durch Kommas getrennt ein',
            required: false,
          },
          {
            name: 'index_',
            placeholder: 'PLZ; Name der Siedlung',
            label: 'PLZ; Name der Siedlung',
            desc: null,
            required: true,
            mask: '##### X*',
          },
          {
            name: 'country',
            placeholder: 'Der Name des Landes',
            label: 'Der Name des Landes',
            desc: null,
            required: true,
          },
        ],
      };
    }
  },
  mounted() {
    this.listFields[this.locale].forEach(el => {
      this.data_form[el.name] = null;
    });
  },
  methods: {
    submit() {}
  }
}
</script>

<style scoped>
.form {
  display: flex;
  flex-direction: column;
  width: 50%;
  margin: 0 auto;
}
</style>
