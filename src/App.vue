<template>
  <Header @getSearch="search = $event" />
  <Notes :notes="filterNotes" @remove="removeNote" @edit="editNote" />
  <Modal
    v-show="showModal"
    @showOrClose="closeModal"
    @addOrChange="addOrChange"
    :title="modalTitle"
    :desc="modalDesc"
    :id="curID"
    @changeTitle="modalTitle = $event"
    @changeDesc="modalDesc = $event"
  />
  <a href="#!" class="openModal" @click="showModal = true">
    <img src="@/assets/img/add-note.svg" alt="">
  </a>
</template>

<script>
import Header from "@/components/Header.vue";
import Notes from "./components/Notes.vue";
import Modal from "./components/Modal.vue";
import { v4 as uuidv4 } from "uuid";

export default {
  name: "App",
  components: {
    Header,
    Notes,
    Modal,
  },
  data() {
    return {
      showModal: false,
      modalTitle: "",
      modalDesc: "",
      curID: null,
      notes: localStorage.notes ? JSON.parse(localStorage.notes) : [],
      search: ""
    };
  },
  computed: {
    filterNotes() {
      return this.search ? this.notes.filter(item => item.title.toLowerCase().includes(this.search.toLowerCase())) : this.notes;
    }
  },
  methods: {
    addOrChange(id) {
      let obj = {
        title: this.modalTitle,
        desc: this.modalDesc,
        id: id || uuidv4(),
        date: new Date(Date.now()).toLocaleDateString(),
      };
      if (id) {
        let idx = this.notes.findIndex(item => item.id == id);
        this.notes[idx] = obj
      } else {
        this.notes.push(obj);
      }
      // console.log(this.notes);
      this.curID = null;
      this.closeModal("close")
      this.save();
    },
    removeNote(id) {
      let idx = this.notes.findIndex((item) => item.id == id);
      // console.log(idx);
      this.notes.splice(idx, 1);
      this.save();
    },
    editNote(id) {
      const obj = this.notes.find(item => item.id == id)
      // console.log(obj);
      this.modalTitle = obj.title;
      this.modalDesc = obj.desc;
      this.curID = obj.id;
      this.showModal = true;
    },
    save() {
      localStorage.notes = JSON.stringify(this.notes)
    },
    closeModal(val) {
      if (val == 'close') {
        this.modalTitle = "";
        this.modalDesc = "";
        this.curID = null;
        this.showModal = !this.showModal
      }
    }
  },
};
</script>

<style lang="scss" scoped>
  .openModal {
    position: fixed;
    bottom: 3rem;
    right: 3rem;
    width: 60px;
    height: 60px;
    display: grid;
    place-items: center;
    background: #fff;
    box-shadow: var(--primaryShadow), var(--secondaryShadow);
    border-radius: 15px;
  }
</style>