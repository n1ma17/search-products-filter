<template>
  <div class="custom-input">
    <label v-if="label" for="custom-input">{{ label }}</label>
    <div ref="inputContainer" class="custom-input__text-field">
      <div
        class="custom-input__text-field__content"
        tabindex="0"
        role="button"
        @click="clickHandler"
        @keydown.enter="clickHandler"
      >
        <input
          id="custom-input"
          ref="input"
          v-model="model"
          :value="value"
          :type="type"
          inputmode="numeric"
          :maxlength="maxlength ? maxlength : null"
          :placeholder="placeholder"
          @input="modelHandler"
        />
      </div>
      <v-btn
        class="pa-0 custom-input__text-field__clear-btn"
        icon
        color="#717972"
        @click="clearValue"
      >
      x
      </v-btn>
    </div>
  </div>
</template>

<script>
import { debounce } from 'lodash'

export default {
  name: 'CustomTextField',

  props: {
    value: {
      type: String,
      default: ''
    },
    label: {
      type: String,
      default: ''
    },
    type: {
      type: String,
      default: ''
    },
    maxlength: {
      type: Number,
      default: null
    },
    placeholder: {
      type: String,
      default: ''
    },
    clearable: {
      type: Boolean,
      default: false
    },
    hasIcon: {
      type: Boolean,
      default: true
    }
  },
  data() {
    return {
      model: ''
    }
  },
  methods: {
    inputDebounced: debounce(function (e) {
      this.model = e
      this.$emit('valueHandler', e)
    }, 500),
    modelHandler(e) {
      this.inputDebounced(e.target.value)
    },
    clearValue() {
      this.model = ''
      this.$emit('valueHandler', '')
    },
    clickHandler() {
      this.$refs.input.focus()
    }
  }
}
</script>

<style lang="scss" scoped>
.custom-input {
  width: 100%;
  display: flex;
  flex-direction: column;
  gap: 8px;
  margin: 8px 0;
  > label {
    font-weight: 600;
    font-size: 14px;
    color: #191c1a;
  }
  &__text-field {
    width: 100%;
    display: flex;
    align-items: center;
    border: 1px solid #d5d5d5;
    border-radius: 12px;
    &:focus-within {
      border-color: #003aaf;
      transition: border-color 0.3s ease-in-out;
    }
    &__content {
      width: 100%;
      height: 100%;
      display: flex;
      align-items: center;
      flex: 1;
      &__prepend-icon {
        margin-left: 12px;
      }
      > input {
        padding: 0 16px;
        width: 100%;
        height: 48px;
        font-size: 16px;
        border: unset;
        text-align: left;
        &:focus {
          box-shadow: none;
          outline: none;
          border: unset;
        }
        &::-webkit-inner-spin-button {
          -webkit-appearance: none;
          margin: 0;
        }
        &::placeholder {
          text-align: left;
        }
      }
    }
    &__clear-btn {
      margin: 0 8px;
    }
  }
}
</style>
