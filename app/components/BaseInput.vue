<template>
    <div class="base-input">
        <label v-if="label" :for="inputId" class="base-input__label">
            {{ label }}
            <span v-if="required" class="base-input__required">*</span>
        </label>

        <div class="base-input__wrapper">
            <div v-if="$slots.prefix || showSearchIcon" class="base-input__icon">
                <slot name="prefix">
                    <svg v-if="showSearchIcon" width="16" height="16" viewBox="0 0 24 24" fill="none"
                        stroke="currentColor" stroke-width="2">
                        <circle cx="11" cy="11" r="8" />
                        <path d="m21 21-4.35-4.35" />
                    </svg>
                </slot>
            </div>

            <input :id="inputId" v-model="inputValue" :type="type" :placeholder="placeholder" :disabled="disabled"
                :readonly="readonly" :required="required" :class="inputClasses" @blur="handleBlur" @focus="handleFocus"
                @input="handleInput" />

            <div v-if="$slots.suffix" class="base-input__suffix">
                <slot name="suffix" />
            </div>
        </div>

        <div v-if="errorMessage" class="base-input__error">
            {{ errorMessage }}
        </div>

        <div v-if="helpText && !errorMessage" class="base-input__help">
            {{ helpText }}
        </div>
    </div>
</template>

<script setup>
import { computed, ref, useId } from 'vue'

const props = defineProps({
    modelValue: {
        type: [String, Number],
        default: ''
    },
    type: {
        type: String,
        default: 'text'
    },
    label: {
        type: String,
        default: ''
    },
    placeholder: {
        type: String,
        default: ''
    },
    disabled: {
        type: Boolean,
        default: false
    },
    readonly: {
        type: Boolean,
        default: false
    },
    required: {
        type: Boolean,
        default: false
    },
    error: {
        type: Boolean,
        default: false
    },
    errorMessage: {
        type: String,
        default: ''
    },
    helpText: {
        type: String,
        default: ''
    },
    size: {
        type: String,
        default: 'medium',
        validator: (value) => ['small', 'medium', 'large'].includes(value)
    },
    showSearchIcon: {
        type: Boolean,
        default: false
    }
})

const emit = defineEmits(['update:modelValue', 'blur', 'focus', 'input'])

const inputId = useId()
const isFocused = ref(false)

const inputValue = computed({
    get: () => props.modelValue,
    set: (value) => emit('update:modelValue', value)
})

const inputClasses = computed(() => [
    'base-input__field',
    `base-input__field--${props.size}`,
    {
        'base-input__field--error': props.error || props.errorMessage,
        'base-input__field--disabled': props.disabled,
        'base-input__field--focused': isFocused.value
    }
])

const handleBlur = (event) => {
    isFocused.value = false
    emit('blur', event)
}

const handleFocus = (event) => {
    isFocused.value = true
    emit('focus', event)
}

const handleInput = (event) => {
    emit('input', event)
}
</script>

<style lang="scss" scoped>
.base-input {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;

    &__label {
        font-size: 0.875rem;
        font-weight: 500;
        color: #374151;
        margin-bottom: 0.25rem;
    }

    &__required {
        color: #ef4444;
        margin-left: 0.125rem;
    }

    &__wrapper {
        position: relative;
        display: flex;
        align-items: center;
    }

    &__field {
        width: 100%;
        border: 1px solid #e5e7eb;
        border-radius: 24px;
        background-color: #f9fafb;
        transition: all 0.2s ease;
        font-size: 0.875rem;
        color: #6b7280;
        padding-left: 2.5rem;

        &::placeholder {
            color: #9ca3af;
        }

        &:focus {
            outline: none;
            border-color: #d1d5db;
            background-color: #ffffff;
            color: #111827;
        }

        &:disabled {
            background-color: #f3f4f6;
            color: #9ca3af;
            cursor: not-allowed;
        }

        &--small {
            padding: 0.75rem 0.75rem 0.75rem 2.5rem;
            font-size: 0.75rem;
            height: 40px;
        }

        &--medium {
            padding: 0.875rem 1rem 0.875rem 2.5rem;
            font-size: 0.875rem;
            height: 48px;
        }

        &--large {
            padding: 1rem 1.25rem 1rem 2.5rem;
            font-size: 1rem;
            height: 56px;
        }

        &--error {
            border-color: #ef4444;
            background-color: #fef2f2;

            &:focus {
                border-color: #ef4444;
                background-color: #ffffff;
            }
        }

        &--focused {
            border-color: #d1d5db;
            background-color: #ffffff;
        }
    }

    &__icon {
        position: absolute;
        left: 0.875rem;
        color: #9ca3af;
        font-size: 1rem;
        pointer-events: none;
    }

    &__suffix {
        position: absolute;
        right: 0.875rem;
        display: flex;
        align-items: center;
        color: #6b7280;
    }

    &__error {
        font-size: 0.75rem;
        color: #ef4444;
        margin-top: 0.25rem;
    }

    &__help {
        font-size: 0.75rem;
        color: #6b7280;
        margin-top: 0.25rem;
    }
}
</style>