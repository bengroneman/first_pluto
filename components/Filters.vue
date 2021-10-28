<template>
    <div class="container">
      <div class="input-group mb-3">
        <label
            class="input-group-text"
            for="inputGroupSelect01"
        >
            Facility
        </label>
        <select
            class="form-select"
            id="inputGroupSelect01"
            v-model="selectedFacility"
        >
          <option selected>Choose...</option>

          <option
                :value="facility"
                v-for="facility in facilities"
                :key="facility"
          >
            {{ facility }}
          </option>
        </select>
      </div>
      <div class="input-group mb-3">
        <label
            class="input-group-text"
            for="departmentSelect"
        >
            Department
        </label>
        <select
            class="form-select"
            id="departmentSelect"
            v-model="selectedDepartment"
        >
          <option selected>Choose...</option>
            <option
                :value="department"
                v-for="department in departments"
                :key="department"
            >
              {{ department }}
            </option>
        </select>
      </div>
    </div>
</template>

<script>
export default {
  data() {
    return {
      // TODO: un-hard code this
      facilities: ['Lander', 'Riverton'],
      departments: [
        'Radiology',
        'Therapy',
        'Workwise',
        'Lab',
        'ER',
        'Rehab',
        'Surgery',
        'OPSC',
        'OB',
        'ICU',
        'Cardiac Rehab',
        'Med Surg',
      ],
      selectedFacility: String,
      selectedDepartment: String,
    };
  },

  // TODO: add validation for these
  emits: ['facilityChanged', 'departmentChanged'],

  // TODO: investigate an easier way to do this
  //       could potentially use the emitter on the select component
  watch: {
    selectedFacility: function(oldFacility, newFacility) {
      this.$emit('facilityChanged', newFacility);
    },

    selectedDepartment: function(oldDepartment, newDepartment) {
      this.$emit('departmentChanged', newDepartment);
    },
  },
};
</script>

