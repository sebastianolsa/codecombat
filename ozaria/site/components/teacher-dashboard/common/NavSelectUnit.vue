<script>
import utils from 'core/utils'

export default {
  props: {
    courses: {
      type: Array,
      default: () => []
    },
    selectedCourseId: {
      type: String,
      default: ''
    }
  },

  computed: {
    isCodeCombat () {
      return utils.isCodeCombat
    },
  },

  methods: {
    i18n (body, key) {
      return utils.i18n(body, key)
    },

    onChange (event) {
      this.$emit('change-course', event.target.value)
    }
  }
}
</script>

<template>
  <div>
    <label>{{ $t('teacher_dashboard.select_' + (isCodeCombat ? 'course' : 'chapter')) }}</label>
    <select @change="onChange($event)">
      <option
        v-for="course in courses"
        :key="course._id"
        :value="course._id"
        :selected="course._id == selectedCourseId"
      >
        {{ i18n(course, 'name') }}
      </option>
    </select>
  </div>
</template>

<style lang="scss" scoped>
@import "app/styles/bootstrap/variables";
@import "ozaria/site/styles/common/variables.scss";
@import "app/styles/ozaria/_ozaria-style-params.scss";

div {
  display: flex;
  flex-direction: column;

  label {
    @include font-p-4-paragraph-smallest-gray;
    font-size: 11px;
    margin-bottom: -2px;
  }
  select {
    @include font-p-2-paragraph-medium-gray;
    font-size: 14px;
    line-height: 20px;
    width: 170px;

    border: 1px solid #379B8D;
    padding: 4px 0;
  }
}
</style>
