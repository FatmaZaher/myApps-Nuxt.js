<template>
  <div class="table-list">
    <b-table
      responsive
      :items="items"
      :fields="fields"
      small
      id="table-list"
      :per-page="perPage"
      :current-page="currentPage"
    >
      <template #cell(id)="data">
        <div class="action">
          <b-button class="" v-if="index">
            <span class="spanId"> {{ data.index }}</span>
          </b-button>
          <b-button
            class="btn main-btn orange-btn"
            v-if="isObjection"
          >
            <nuxt-link :to="'/Reports/Objections/objectionSubmit'">
              إعتراض
            </nuxt-link>
          </b-button>
          <b-button class="btn main-btn" v-if="isJustification">
            <nuxt-link :to="'/Reports/Justifications/JustificationSubmit'">
              تبرير
            </nuxt-link>
          </b-button>
          <b-button v-if="isShow" class="specialbtn">
            <ShowIcon />
          </b-button>
          <b-button @click="editModal" v-if="isEdit" class="specialbtn">
            <EditIcon />
            <AddModal
              v-model="editmodal"
              :save-button="false"
              :compliance-record="complianceRecord"
              size=""
            />
          </b-button>
          <b-button @click="deleteModal" v-if="isDelete" class="specialbtn">
            <TrashIcon />
            <AddModal
              v-model="deletemodal"
              :buttonTitle="deleteTitle"
              :is-delete-modal="true"
              :save-button="false"
              :delete-text="deleteText"
              size=""
            />
          </b-button>
        </div>
      </template>
      <template #cell(actual)="data">
        <div class="action">
          <b-button v-if="index">
            <span class="spanId"> {{ data.index }}</span>
          </b-button>
          <b-button @click="actualModal" class="specialbtn">
            <FileIcon />
            <AddModal
              v-model="actualmodal"
              :is-actual="true"
              :save-button="false"
              size=""
            />
          </b-button>
        </div>
      </template>
      <template #cell(qualityManagerNotes)="data">
        <div class="action">
          <b-button v-if="index">
            <span class="spanId"> {{ data.index }}</span>
          </b-button>
          <b-button @click="qualityModal" class="specialbtn">
            <FileIcon />
            <AddModal
              v-model="qualitymodal"
              :is-quality-notes="true"
              :save-button="false"
              size=""
            />
          </b-button>
        </div>
      </template>
      <template #cell(stakeholderNotes)="data">
        <div class="action">
          <b-button v-if="index">
            <span class="spanId"> {{ data.index }}</span>
          </b-button>
          <b-button @click="stakeholderModal" class="specialbtn">
            <FileIcon />
            <AddModal
              v-model="stakeholdermodal"
              :is-stakeholder-notes="true"
              :save-button="false"
              size=""
            />
          </b-button>
        </div>
      </template>
      <template #cell(justification)="data">
        <div>
          <b-button v-if="index">
            <span class="spanId"> {{ data.index }}</span>
          </b-button>
          <nuxt-link :to="'/Reports/Justifications/JustificationText'">
            <FileIcon />
          </nuxt-link>
        </div>
      </template>
      <template #cell(objectionReson)="data">
        <div>
          <b-button v-if="index">
            <span class="spanId"> {{ data.index }}</span>
          </b-button>
          <nuxt-link :to="'/Reports/Objections/ObjectionText'">
            <FileIcon />
          </nuxt-link>
        </div>
      </template>
      <template #cell(actionText)="data">
        <div>
          <b-button v-if="index">
            <span class="spanId"> {{ data.index }}</span>
          </b-button>
          <nuxt-link :to="'/Action/ActionText'">
            <FileIcon />
          </nuxt-link>
        </div>
      </template>
      <template #cell(all)="data">
        <div class="action">
          <b-button v-if="index">
            <span class="spanId"> {{ data.index }}</span>
          </b-button>
          <b-form-checkbox
            v-model="allChecked"
            name="check-button"
            switch
            class="allCheck"
          >
          </b-form-checkbox>
        </div>
      </template>
      <template #cell(view)="data">
        <div>
          <b-button v-if="index">
            <span class="spanId"> {{ data.index }}</span>
          </b-button>
          <b-form-checkbox v-model="viewChecked" name="check-button" switch>
          </b-form-checkbox>
        </div>
      </template>
      <template #cell(save)="data">
        <div>
          <b-button v-if="index">
            <span class="spanId"> {{ data.index }}</span>
          </b-button>
          <b-form-checkbox v-model="saveChecked" name="check-button" switch>
          </b-form-checkbox>
        </div>
      </template>
      <template #cell(edit)="data">
        <div>
          <b-button v-if="index">
            <span class="spanId"> {{ data.index }}</span>
          </b-button>
          <b-form-checkbox v-model="editChecked" name="check-button" switch>
          </b-form-checkbox>
        </div>
      </template>
      <template #cell(print)="data">
        <div>
          <b-button v-if="index">
            <span class="spanId"> {{ data.index }}</span>
          </b-button>
          <b-form-checkbox v-model="printChecked" name="check-button" switch>
          </b-form-checkbox>
        </div>
      </template>
      <template #cell(delete)="data">
        <div>
          <b-button v-if="index">
            <span class="spanId"> {{ data.index }}</span>
          </b-button>
          <b-form-checkbox v-model="deleteChecked" name="check-button" switch>
          </b-form-checkbox>
        </div>
      </template>
    </b-table>
    <div class="pagin d-flex justify-content-center">
      <b-pagination
        v-model="currentPage"
        :total-rows="rows"
        :per-page="perPage"
        aria-controls="table-list"
      ></b-pagination>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    items: {
      type: Array,
      default: [],
    },
    rows: {
      type: null,
      default: '',
    },
    fields: {
      type: Array,
      default: [],
    },
    rows: {
      type: null,
      default: '',
    },
    index: {
      type: Boolean,
      default: false,
    },
    id: {
      type: null,
      default: '',
    },
    isObjection: {
      type: Boolean,
      default: false,
    },
    isJustification: {
      type: Boolean,
      default: false,
    },
    isDelete: {
      type: Boolean,
      default: false,
    },
    isShow: {
      type: Boolean,
      default: false,
    },
    isEdit: {
      type: Boolean,
      default: false,
    },
    deleteText: {
      type: String,
      default: 'هل أنت متأكد من عملية الحذف؟',
    },
    complianceRecord: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      perPage: 3,
      currentPage: 1,
      deletemodal: false,
      actualmodal: false,
      qualitymodal: false,
      editmodal: false,
      stakeholdermodal: false,
      showTitle: 'عرض',
      deleteTitle: 'تأكيد الحذف',
      allChecked: false,
      viewChecked: false,
      saveChecked: false,
      editChecked: false,
      deleteChecked: false,
      printChecked: false,
    }
  },
  methods: {
    deleteModal() {
      this.deletemodal = true
    },
    actualModal() {
      this.actualmodal = true
    },
    qualityModal() {
      this.qualitymodal = true
    },
    editModal() {
      this.editmodal = true
    },
    stakeholderModal() {
      this.stakeholdermodal = true
    },
  },
}
</script>
<style lang="scss" scoped>
@import '~/assets/scss/style.scss';
</style>
