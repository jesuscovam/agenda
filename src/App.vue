<template>
  <mdb-container>
    <mdb-row class="top">
      <mdb-col col="9">
        <h2 class="text-uppercase my-3">Hoy:</h2>
        <Evento
          v-for="(event, index) in events"
          :time="event.time"
          :title="event.title"
          :location="event.location"
          :description="event.description"
          :key="index"
          :index="index"
          @delete="handleDelete"
        />
        <mdb-row>
          <mdb-col xl="3" md="6" class="mx-auto text-center">
            <mdb-btn @click.native="modal = true" color="info"
              >Agregar
            </mdb-btn>
          </mdb-col>
        </mdb-row>
      </mdb-col>
      <mdb-col col="3">
        <h3 class="text-uppercase my-3">Horario</h3>
        <h6 class="my-3">
          <div v-if="length >= 4">
            Va a ser un día ocupado. Tienes
            <b>{{ length }} eventos</b> hoy
          </div>
          <div v-else-if="length === 0">
            Hoy no tienes eventos
          </div>
          <div v-else>
            Hoy tienes
            <b> {{ length }} eventos</b>
          </div>
        </h6>
        <h1 class="my-3">
          <mdb-row>
            <mdb-col col="3" class="text-center">
              <mdb-icon far icon="sun" />
            </mdb-col>
          </mdb-row>
          <mdb-row>
            <mdb-col col="3" class="text-center">
              <mdb-icon icon="thermometer-three-quarters" />
            </mdb-col>
            <mdb-col col="9">33°C</mdb-col>
          </mdb-row>
        </h1>
      </mdb-col>
    </mdb-row>
    <mdb-modal v-if="modal" @close="modal = false">
      <mdb-modal-header>
        <mdb-modal-title tag="h4" class="w-100 text-center font-weight-bold">
          Agregar nuevo evento
        </mdb-modal-title>
      </mdb-modal-header>
      <mdb-modal-body>
        <form class="mx-3 grey-text">
          <mdb-input
            name="time"
            label="Tiempo"
            icon="clock"
            placeholder="12:30"
            type="text"
            v-model="newValues.time"
          />
          <mdb-input
            name="title"
            label="Titulo"
            icon="edit"
            placeholder="Cita"
            type="text"
            v-model="newValues.title"
          />
          <mdb-input
            name="location"
            label="Locación"
            icon="map"
            placeholder="Lugar"
            type="text"
            v-model="newValues.location"
          />
          <mdb-textarea
            name="description"
            label="Descripción"
            icon="sticky-note"
            v-model="newValues.description"
          />
        </form>
      </mdb-modal-body>
      <mdb-modal-footer class="justify-content-center">
        <mdb-btn color="info" @click.native="addEvent">
          Agregar
        </mdb-btn>
      </mdb-modal-footer>
    </mdb-modal>
  </mdb-container>
</template>

<script>
import {
  mdbContainer,
  mdbRow,
  mdbCol,
  mdbBtn,
  mdbIcon,
  mdbModal,
  mdbModalHeader,
  mdbModalTitle,
  mdbModalBody,
  mdbModalFooter,
  mdbInput,
  mdbTextarea
} from "mdbvue";

import Evento from "./components/Event";
export default {
  name: "App",
  components: {
    mdbContainer,
    mdbRow,
    mdbCol,
    Evento,
    mdbIcon,
    mdbBtn,
    mdbModal,
    mdbModalHeader,
    mdbModalTitle,
    mdbModalBody,
    mdbModalFooter,
    mdbInput,
    mdbTextarea
  },
  data() {
    return {
      events: [
        {
          time: "10:00",
          title: "Nadar",
          location: "Piscina condominio",
          description: "Nadar media hora"
        },
        {
          time: "11:00",
          title: "Matecito con Boro",
          location: "Casa"
        },
        {
          time: "12:00",
          title: "Trabajar en proyecto grupal"
        },
        {
          time: "2:00",
          title: "Almuerzo con Michel",
          location: "Peace&Bowl Calle 30 entre Av 30 y 25",
          description: "Almuerzo con el Mich"
        }
      ],
      modal: false,
      newValues: {
        time: "",
        title: "",
        location: "",
        description: ""
      }
    };
  },
  methods: {
    handleDelete(eventIndex) {
      this.events.splice(eventIndex, 1);
    },
    addEvent() {
      this.events.push(this.newValues);
      this.newValues = [];
      this.modal = false;
    }
  },
  computed: {
    length() {
      return this.events.length;
    }
  }
};
</script>

<style>
.top {
  margin-top: 40px;
}
</style>
