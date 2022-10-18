<!-- Hier steht unser Template für unsere Komponente -->
<template>
  <li>
    <h2>{{ name }} {{ isFavorite ? " **Favorite**" : "" }}</h2>
    <button @click="toggleDetails">
      {{ detailsAreVisible ? "Hide" : "Show" }} Details
    </button>
    <button @click="toggleFavorite">Toggle Favorite</button>
    <ul v-if="detailsAreVisible">
      <li>
        <strong>Phone:</strong>
        {{ phoneNumber }}
      </li>
      <li>
        <strong>Email:</strong>
        {{ emailAddress }}
      </li>
    </ul>
  </li>
</template>

<script>
export default {
  // props können als array angegeben werden
  // props: ['name','phoneNumber','emailAddress','isFavorite'],

  // props können als Objekte mit speziellen Eigenschaften angegeben werden
  props: {
    id: {
      type: String,
      required: true,
    },
    name: {
      type: String,
      required: true,
    },
    phoneNumber: {
      type: String,
      required: true,
    },
    emailAddress: {
      type: String,
      required: true,
    },
    isFavorite: {
      type: Boolean,
      required: false,
      default: false,
    },
  },

  // NEU(2) definieren der Events wird empfohlen, ist aber nicht zwingend
  // es dient der Dokumentation der Komponente und vorallem für "andere" Programmierer
  // es gibt die array Methode um events aufzulisten ['toggle-favorite', ....],
  emits: ['toggle-favorite'],

  // Kommentieren mit STRG+K+C bzw. STRG+K+U 
  // emits: {
  //   // "toggle-favorite": function (id) {},
  //   // oder noch detailierter:

  //   "toggle-favorite": function (id) {
  //     if (id) return true;
  //     else {
  //       console.warn("id is missing");
  //       return false;
  //     }
  //   },
  // },

  data() {
    return {
      detailsAreVisible: false,
    };
  },

  methods: {
    toggleDetails() {
      this.detailsAreVisible = !this.detailsAreVisible;
    },
    toggleFavorite() {
      alert("inside FriendContags   toggleFavorite works");
      // NEU(1)
      // $emit ist eingebaute Funktion in vue.
      // event namen immer in kebap-case, also 'toggle-favorite', siehe unten
      // Das funktioniert wie bei einem normalen Button, der einen click-Event auslöst

      this.$emit("toggle-favorite", this.id);
    },
  },
};
</script>