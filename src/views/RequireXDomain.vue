<template>
  <div class="container">
    <div id="domainMessage" class="alert alert-danger" role="alert" style="display: none">
      <span></span>
    </div>

    <div class="container text-left">
      <button class="btn" @click="onGoBack">
        <i class="fa fa-arrow-left"></i>
        <small class="mx-2">{{ $t("requirex_go_back") }}</small>
      </button>
    </div>

    <div class="my-3">
      <h2>{{$t("requirex_domain_tittle")}}</h2>
    </div>

    <div class="container my-2 form-requirement">
      <form id="domainForm" ref="requirement">
        <div class="row">
          <div class="col">
            <label for="reqType">
              <font size="3" color="red">*</font>
              {{$t('requirex_requirement_type_label')}}
            </label>

            <select id="reqType" v-model="requirement.reqType" class="form-control">
              <option
                :value="$t('requirex_requirement_type_value_1')"
              >{{ $t('requirex_requirement_type1')}}</option>
              <option
                :value="$t('requirex_requirement_type_value_2')"
              >{{ $t('requirex_requirement_type2')}}</option>
              <option
                :value="$t('requirex_requirement_type_value_3')"
              >{{ $t('requirex_requirement_type3')}}</option>
            </select>
          </div>
          <div class="col">
            <label for="affectedSystems">
              <font size="3" color="red">*</font>
              {{$t('requirex_requirement_affected_systems_label')}}
            </label>

            <select
              id="affectedSystems"
              v-model="requirement.affectedSystems"
              @change="onaffectedSystemsChange"
              class="form-control"
            >
              <option
                :value="$t('requirex_requirement_affected_systems1')"
                selected
              >{{ $t('requirex_requirement_affected_systems1')}}</option>
              <option
                :value="$t('requirex_requirement_affected_systems2')"
              >{{ $t('requirex_requirement_affected_systems2')}}</option>
              <option
                :value="$t('requirex_requirement_affected_systems3')"
              >{{ $t('requirex_requirement_affected_systems3')}}</option>
            </select>
          </div>
        </div>

        <div id="thoseCoditionContainer" class="form-group my-3" style="display: none">
          <label for="thoseCodition">{{$t('requirex_requirement_affected_condition')}}</label>
          <input
            id="thoseCodition"
            v-model="requirement.thoseCodition"
            class="form-control"
            :placeholder="$t('requirex_requirement_affected_condition')"
          />
        </div>

        <div class="row my-2">
          <div class="col">
            <label>
              <font size="3" color="red">*</font>
              {{$t('requirex_requirement_system_domain_name_label')}}
            </label>
            <input
              id="systemName"
              v-model="requirement.systemName"
              class="form-control"
              :placeholder="$t('requirex_requirement_system_domain_name_label')"
            />
          </div>
          <div class="col">
            <label>
              <font size="3" color="red">*</font>
              {{$t('requirex_requirement_name_label')}}
            </label>
            <input
              id="name"
              v-model="requirement.name"
              class="form-control"
              :placeholder="$t('requirex_requirement_name_label')"
            />
          </div>
        </div>

        <div class="row my-2">
          <div class="col">
            <div class="custom-control custom-switch">
              <input
                type="checkbox"
                class="custom-control-input"
                id="condition"
                v-model="requirement.condition"
                value="false"
                @click="onConditionCheck"
              />
              <label
                class="custom-control-label"
                for="condition"
              >{{$t('requirex_requirement_condition_label')}}</label>
            </div>
          </div>
          <div id="conditionDescriptionContainer" class="col" style="display: none">
            <textarea
              id="conditionDescription"
              v-model="requirement.conditionDescription"
              class="form-control"
              type="textarea"
              :autosize="{minRows: 2,maxRows: 5}"
              :placeholder="$t('requirex_requirement_condition_descrive_label')"
            />
          </div>
        </div>

        <div class="row">
          <div class="col">
            <label>
              <font size="3" color="red">*</font>
              {{ $t('requirex_requirement_imperative_label') }}
            </label>
            <select id="imperative" v-model="requirement.imperative" class="form-control">
              <option
                :value="$t('requirex_requirement_imperative_value_1')"
              >{{ $t('requirex_requirement_imperative1') }}</option>
              <option
                :value="$t('requirex_requirement_imperative_value_2')"
              >{{ $t('requirex_requirement_imperative2')}}</option>
              <option
                :value="$t('requirex_requirement_imperative_value_3')"
              >{{ $t('requirex_requirement_imperative3')}}</option>
            </select>
          </div>

          <div class="col">
            <label class="text-left">
              <font size="3" color="red">*</font>
              {{ $t('requirex_requirement_system_activity_label') }}
            </label>
            <select
              id="systemActivity"
              v-model="requirement.systemActivity"
              class="form-control"
              @change="onSystemActivityChange"
            >
              <option
                :value="$t('requirex_requirement_system_activity_value_1')"
              >{{ $t('requirex_requirement_system_activity1')}}</option>
              <option
                :value="$t('requirex_requirement_system_activity_value_2')"
              >{{ $t('requirex_requirement_system_activity2')}}</option>
              <option
                :value="$t('requirex_requirement_system_activity_value_3')"
              >{{ $t('requirex_requirement_system_activity3')}}</option>
            </select>
          </div>
        </div>

        <div id="userContent" class="text-left my-2">
          <label>{{$t('requirex_requirement_user_label')}}</label>
          <input
            id="user"
            v-model="requirement.user"
            class="form-control"
            :placeholder="$t('requirex_requirement_user_label')"
          />
        </div>

        <div id="extIntContent" class="row my-2" style="display: none">
          <div class="col">
            <label>{{$t('requirex_requirement_system_label')}}</label>
            <input
              id="system"
              v-model="requirement.system"
              class="form-control"
              :placeholder="$t('requirex_requirement_system_label')"
            />
          </div>
          <div class="col">
            <label>{{ $t('requirex_requirement_from_label') }}</label>
            <select
              id="from"
              v-model="requirement.from"
              class="form-control"
              :placeholder="$t('requirex_select')"
            >
              <option
                :value="$t('requirex_requirement_from_value_1')"
              >{{ $t('requirex_requirement_from1')}}</option>
              <option
                :value="$t('requirex_requirement_system_from_value_2')"
              >{{ $t('requirex_requirement_from2')}}</option>
            </select>
          </div>
        </div>

        <div class="row">
          <div class="col">
            <label>
              <font size="3" color="red">*</font>
              {{ $t('requirex_requirement_process_verb_label') }}
            </label>
            <input
              id="processVerb"
              v-model="requirement.processVerb"
              class="form-control"
              :placeholder="$t('requirex_requirement_process_verb_label')"
            />
          </div>
          <div class="col">
            <label>
              <font size="3" color="red">*</font>
              {{ $t('requirex_requirement_object_label') }}
            </label>
            <input
              id="object"
              v-model="requirement.object"
              class="form-control"
              :placeholder="$t('requirex_requirement_object_label')"
            />
          </div>
        </div>

        <div class="custom-control custom-switch my-2">
          <input
            type="checkbox"
            class="custom-control-input"
            id="systemCondition"
            v-model="requirement.systemCondition"
            @click="onSystemConditionCheck"
          />
          <label
            class="custom-control-label"
            for="systemCondition"
          >{{$t('requirex_requirement_system_condition_domain_label')}}</label>
        </div>

        <div id="systemConditionDescriptionContainer" class="text-left" style="display: none">
          <label>{{ $t('requirex_requirement_description') }}</label>
          <textarea
            id="systemConditionDescription"
            v-model="requirement.systemConditionDescription"
            class="form-control"
            type="textarea"
            :autosize="{minRows: 2,maxRows: 5}"
            :placeholder="$t('requirex_requirement_system_condition_descrive_label')"
          />
        </div>
      </form>

      <div class="container text-right my-2">
        <button
          id="generate"
          @click="onGenerateRequirement"
          type="button"
          class="btn btn-outline-dark mx-2"
        >{{$t('requirex_generate')}}</button>
        <button id="cancel" type="button" class="btn btn-danger">{{$t('requirex_cancel')}}</button>
      </div>
    </div>
  </div>
</template>
<script src="//vuejs.org/js/vue.min.js"></script>
<script src="//unpkg.com/iview/dist/iview.min.js"></script>

<script>
import $ from "jquery";
import axios from 'axios';

$(function() {
  //Agregar o retirar condiciones del sistema
  $(document).on("click", "#cancel", function() {
    $("#domainForm").trigger("reset");
  });
});

export default {
  data() {
    return {
      listDomainRequirement: [],
      countDomain: 0,
      requirement: {
        id: 0,
        requirementNumber: "",
        affectedSystems: this.$t("requirex_requirement_affected_systems1"),
        thoseCodition: "",
        isThoseCodition: false,
        reqType: this.$t("requirex_requirement_type_value_1"),
        name: "",
        condition: false,
        conditionDescription: "",
        imperative: this.$t("requirex_requirement_imperative_value_1"),
        systemName: "",
        systemActivity: this.$t("requirex_requirement_system_activity_value_1"),
        user: "",
        processVerb: "",
        object: "",
        system: "",
        from: this.$t("requirex_requirement_from_value_1"),
        systemCondition: false,
        systemConditionDescription: "",
        msg: "",
        estado: true,
        date_at: new Date().toISOString().slice(0, 10)
      }
    };
  },
  methods: {
    //Alcambiar Los sistemas afectados
    onaffectedSystemsChange() {
      alert(this.requirement.affectedSystems);
      if (
        this.requirement.affectedSystems ==
        this.$t("requirex_requirement_affected_systems3")
      ) {
        $("#thoseCoditionContainer")
          .first()
          .fadeIn("slow");

        this.requirement.isThoseCodition = true;
      } else {
        this.requirement.isThoseCodition = false;
        $("#thoseCoditionContainer").hide();
      }
    },
    //Activar condiciones
    onConditionCheck() {
      console.log("entro");
      if ($("#condition").is(":checked")) {
        $("#conditionDescriptionContainer")
          .first()
          .fadeIn("slow");

        this.requirement.condition = true;
      } else {
        this.requirement.condition = false;
        $("#conditionDescriptionContainer").hide();
      }
    },
    //Activar condiciones
    onSystemConditionCheck() {
      if ($("#systemCondition").is(":checked")) {
        $("#systemConditionDescriptionContainer")
          .first()
          .fadeIn("slow");
        this.requirement.systemCondition = true;
      } else {
        this.requirement.systemCondition = false;
        $("#systemConditionDescriptionContainer").hide();
      }
    },
    onSystemActivityChange() {
      if (this.requirement.systemActivity == "userInt") {
        $("#userContent")
          .first()
          .fadeIn("slow");
        $("#extIntContent").hide();
      } else if (this.requirement.systemActivity == "autoAct") {
        //Al selecccionar actividad autonoma
        $("#userContent").hide();
        $("#extIntContent").hide();
      } else if (this.requirement.systemActivity == "extInt") {
        //Al seleccionar actividad externa
        $("#userContent").hide();
        $("#extIntContent")
          .first()
          .fadeIn("slow");
      }
    },
    onGenerateRequirement() {
      //Reiniciar requerimiento
      this.requirement.msg = "";

      //Si hay una condición
      if (this.requirement.condition == true) {
        this.requirement.msg += this.requirement.conditionDescription + " ";
      }

      //Sistemas afectado
      this.requirement.msg += this.requirement.affectedSystems + " ";
      //Complemento
      this.requirement.msg += this.$t(
        "requirex_requirement_affected_systems_complement"
      );

      if (
        this.requirement.affectedSystems ==
        this.$t("requirex_requirement_affected_systems3")
      ) {
        this.requirement.msg +=
          this.$t("requirex_requirement_affected_that") + " ";
        this.requirement.msg += this.requirement.thoseCodition + " ";
      }

      this.requirement.msg +=
        this.requirement.systemName + " " + this.requirement.imperative;

      //Validate system activity
      if (this.requirement.systemActivity == "autoAct") {
        this.requirement.msg +=
          " " + this.requirement.processVerb + " " + this.requirement.object;
      } else if (this.requirement.systemActivity == "userInt") {
        this.requirement.msg +=
          " provide the " + this.requirement.user + " with the capacity of";
        this.requirement.msg +=
          " " + this.requirement.processVerb + " " + this.requirement.object;
      } else if (this.requirement.systemActivity == "extInt") {
        this.requirement.msg +=
          " have the capacity of " +
          this.requirement.processVerb +
          " " +
          this.requirement.object +
          " " +
          this.requirement.from +
          " the " +
          this.requirement.system;
      }

      //Validat conditions
      if (this.requirement.systemCondition) {
        this.requirement.msg +=
          ", " + this.requirement.systemConditionDescription;
      }
      //Agregar item a la lista
      this.countDomain++;
      this.requirement.id = this.countDomain;
      this.requirement.requirementNumber = "D.R." + this.requirement.id;
      this.requirement.date_at = new Date().toISOString().slice(0, 10);

      this.saveRequirement();

      //Contar Requerimientos

      $("#domainMessage span").text("Success!");
      $("#domainMessage").addClass("alert-success");
      $("#domainMessage").removeClass("alert-danger");
      setTimeout(this.showTooltip, 500);

      $("#domainForm").trigger("reset");
    },
    showTooltip() {
      $("#domainMessage").show("slow");
      setTimeout(this.hideTooltip, 5000);
    },

    hideTooltip() {
      $("#domainMessage").hide("slow");
    },
    saveRequirement() {
      let uri = localStorage["domain_implementation_main_path"] + "requirex/domains";
      axios.post(uri, this.requirement).then(() => {
        this.$Message.success("Success!");
        this.$router.push("/requirex");
      });
    },
    onGoBack() {
      this.$router.push({
        name: "RequireX"
      });
    }
  },
  created() {
    //Cargar lista de requerimientos de dominio
    let uri = localStorage["domain_implementation_main_path"] + "requirex/domains";
    axios.get(uri).then(response => {
      this.listDomainRequirement = response.data;
      this.countDomain = this.listDomainRequirement.length;
      console.log("total dominio" + this.countDomain);
    });
  }
};
</script>

<style scoped>
.form-requirement {
  margin: 0 auto;
  max-width: 500px;
}

.error {
  border: 1px solid red;
}
</style>
