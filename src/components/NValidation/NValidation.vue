<template>
  <div v-if="!isHidden" class="n-validation-container" :class="validatorClass">
    <nitrozen-icon class="n-validator-icon" :color="getValidatorIconColor" :name="validationState" :size="size" />
    <span>{{ label }}</span>
  </div>
</template>

<script>
import NIcon from '../NIcon';
export default {
  name: 'nitrozen-validation',
  components: {
    'nitrozen-icon': NIcon,
  },
  props: {
    validationState: {
      type: String,
      default: 'default',
      validator(value) {
        // The value must match one of these strings
        return ['success', 'warning', 'error', 'default', 'info'].includes(value)
      }
    },
    label: {
      type: String,
      default: "Default Label"
    },
    isHidden: {
      type: Boolean,
      default: false
    },
    size: {
      type: Number,
      default: 16
    }
  },
  computed: {
    validatorClass() {
      return {
        'n-validation-success':
          this.$props.validationState.toLowerCase() === 'success',
        'n-validation-error':
          this.$props.validationState.toLowerCase() === 'error',
        'n-validation-warning':
          this.$props.validationState.toLowerCase() === 'warning',
      };
    },
    getValidatorIconColor() {
      let colorMap = {
        success: '#25ab21',
        error: '#f50031',
        warning: '#7d2f08',
      };
      return colorMap[this.$props.validationState];
    },
  },
};
</script>

<style scoped lang="less">
@import url('../../base/base.less');

.n-validator-icon {
  margin-right: 8px;
}

.n-validation-container {
  display: flex;
  justify-content: center;
  align-items: center;
  width: fit-content;
  height: fit-content;
  font-family: "JioType", helvetica, arial, sans-serif;
  font-weight: 500;
  text-transform: none;
  font-size: 14px;
  letter-spacing: -0.07px;
}

.n-validation-success {
  color: @ColorFeedbackSuccess80;

  svg {
    fill: @ColorFeedbackSuccess50;
  }
}

.n-validation-error {
  color: @ColorFeedbackError80;

  svg {
    fill: @ColorFeedbackError50;
  }
}

.n-validation-warning {
  color: @ColorFeedbackWarning80;

  svg path {
    fill: @ColorFeedbackWarning50;
  }
}

.n-validation-default {
  color: #141414;
}
</style>
