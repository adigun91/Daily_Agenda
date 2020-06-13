<template>
  <mdb-container class="col, size">
    <mdb-row>
      <mdb-col col="9">
        <h2 class="text-uppercase my-3, pad">Daily_Agenda_Organizer:</h2>
        <Event
          v-for="(event, index) in events"
          :index="index"
          :time="event.time"
          :title="event.title"
          :location="event.location"
          :description="event.description"
          :key="index"
          @delete="handleDelete"
        />
        <mdb-row>
          <mdb-col xl="3" md="6" class="mx-auto text-center">
            <mdb-btn color="info" @click.native="modal = true">Add Event</mdb-btn>
          </mdb-col>
        </mdb-row>
      </mdb-col>
      <mdb-col col="3">
        <h5 class="text-uppercase my-3">Schedule for the Day</h5>
        <h6 class="my-3">
          It's going to be busy that today. You have
          <b>{{events.length}} events</b> today.
        </h6>
        <h1 class="my-3">
          <mdb-row>
            <mdb-col col="3" class="text-center">
              <mdb-icon far icon="sun"/>
            </mdb-col>
            <mdb-col col="9">Sunny</mdb-col>
          </mdb-row>
          <mdb-row>
            <mdb-col col="3" class="text-center">
              <mdb-icon icon="thermometer-three-quarters"/>
            </mdb-col>
            <mdb-col col="9">
              23°C
            </mdb-col>
          </mdb-row>
        </h1>
        <p>
          Don't forget your sunglasses. Today will dry and sunny, becoming
          warm in the afternoon with temperatures of between 20 and 25
          degrees.
        </p>
      </mdb-col>
    </mdb-row>

    <mdb-modal v-if="modal" @close="modal = false">
      <mdb-modal-header>
        <mdb-modal-title tag="h4" class="w-100 text-center font-weight-bold">Add New Agenda</mdb-modal-title>
      </mdb-modal-header>
      <mdb-modal-body>
        <form class="mx-3 grey-text">
          <mdb-input
            name="time"
            label="Time"
            icon="clock"
            placeholder="12:30"
            type="text"
            @input="handleInput($event, 'time')"
          />
          <mdb-input
            name="title"
            label="Title"
            icon="edit"
            placeholder="Briefing"
            type="text"
            @input="handleInput($event, 'title')"
          />
          <mdb-input
            name="location"
            label="Location (optional)"
            icon="map"
            type="text"
            @input="handleInput($event, 'location')"
          />
          <mdb-textarea
            name="description"
            label="Description (optional)"
            icon="sticky-note"
            @input="handleInput($event, 'description')"
          />
        </form>
      </mdb-modal-body>
      <mdb-modal-footer class="justify-content-center">
        <mdb-btn color="info" @click.native="addEvent">Add Agenda</mdb-btn>
      </mdb-modal-footer>
    </mdb-modal>
  </mdb-container>
</template>

<script>
import {
  mdbContainer,
  mdbRow,
  mdbCol,
  mdbIcon,
  mdbBtn,
  mdbModal,
  mdbModalHeader,
  mdbModalTitle,
  mdbModalBody,
  mdbModalFooter,
  mdbInput,
  mdbTextarea
} from "mdbvue";
import Event from "@/components/Event";
export default {
  name: "App",
  components: {
    mdbContainer,
    mdbRow,
    mdbCol,
    mdbIcon,
    mdbBtn,
    mdbModal,
    mdbModalHeader,
    mdbModalTitle,
    mdbModalBody,
    mdbModalFooter,
    mdbInput,
    mdbTextarea,
    Event
  },
  data() {
    return {
      events: [
        {
          time: "05:00",
          title: "Family Devotion",
          location: "Sitting room",
          description: "Commit our day, lives and everything we are to do today into God's Hand"
        },
        {
          time: "07:30",
          title: "Breakfast with family",
          location: "Dining Room"
        },
        {
          time: "07:45",
          title: "Leave for Office"
        },
        {
          time: "12:00",
          title: "Lunch with Hannah",
          location: "Eatery",
          description: "Talk about our live together"
        }
      ],
      modal: false,
      newValues: []
    };
  },
  methods: {
    handleDelete(eventIndex) {
      this.events.splice(eventIndex, 1);
    },
    handleInput(val, type) {
      this.newValues[type] = val;
    },
    addEvent() {
      this.events.push({
        time: this.newValues["time"],
        title: this.newValues["title"],
        location: this.newValues["location"],
        description: this.newValues["description"]
      });
    }
  }
};
</script>

<style>
.col{
  background-color: rgb(255, 255, 255);
}
.size{
  width: 80%;
}
.pad{
  margin: 20px 0px 15px 0px
}
</style>