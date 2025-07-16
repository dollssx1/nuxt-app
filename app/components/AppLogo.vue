<template>
  <!-- 채대원 소프트 로고 컴포넌트 -->
  <div class="app-logo" :class="logoClasses">
    <!-- 로고 아이콘 부분 -->
    <div class="app-logo__icon">
      <svg width="32" height="32" viewBox="0 0 32 32" fill="none">
        <!-- C 모양의 메인 아이콘 -->
        <circle cx="16" cy="16" r="14" stroke="currentColor" stroke-width="2" fill="none" stroke-dasharray="22 10"/>
        <!-- 내부 점 -->
        <circle cx="16" cy="16" r="4" fill="currentColor"/>
        <!-- 소프트웨어를 상징하는 작은 점들 -->
        <circle cx="8" cy="12" r="1" fill="currentColor" opacity="0.6"/>
        <circle cx="24" cy="12" r="1" fill="currentColor" opacity="0.6"/>
        <circle cx="8" cy="20" r="1" fill="currentColor" opacity="0.6"/>
        <circle cx="24" cy="20" r="1" fill="currentColor" opacity="0.6"/>
      </svg>
    </div>
    
    <!-- 로고 텍스트 부분 -->
    <div class="app-logo__text">
      <span class="app-logo__main">채대원</span>
      <span class="app-logo__sub">소프트</span>
    </div>
  </div>
</template>

<script setup>
// 로고 크기 및 스타일 props 정의
const props = defineProps({
  // 로고 크기 (small, medium, large)
  size: {
    type: String,
    default: 'medium',
    validator: (value) => ['small', 'medium', 'large'].includes(value)
  },
  // 세로형 레이아웃 여부
  vertical: {
    type: Boolean,
    default: false
  },
  // 텍스트만 표시 (아이콘 숨김)
  textOnly: {
    type: Boolean,
    default: false
  },
  // 아이콘만 표시 (텍스트 숨김)
  iconOnly: {
    type: Boolean,
    default: false
  }
})

// 로고 클래스 계산
const logoClasses = computed(() => [
  `app-logo--${props.size}`,
  {
    'app-logo--vertical': props.vertical,
    'app-logo--text-only': props.textOnly,
    'app-logo--icon-only': props.iconOnly
  }
])
</script>

<style lang="scss" scoped>
.app-logo {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  color: #1f2937;
  text-decoration: none;
  transition: all 0.2s ease;

  // 호버 효과
  &:hover {
    color: #3b82f6;
    transform: translateY(-10px);
  }

  // 세로형 레이아웃
  &--vertical {
    flex-direction: column;
    text-align: center;
    gap: 0.5rem;
  }

  // 텍스트만 표시
  &--text-only {
    .app-logo__icon {
      display: none;
    }
  }

  // 아이콘만 표시
  &--icon-only {
    .app-logo__text {
      display: none;
    }
  }

  // 아이콘 스타일
  &__icon {
    display: flex;
    align-items: center;
    justify-content: center;
    color: #3b82f6;
    
    svg {
      transition: transform 0.2s ease;
    }

    &:hover svg {
      transform: rotate(5deg);
    }
  }

  // 텍스트 컨테이너
  &__text {
    display: flex;
    flex-direction: column;
    line-height: 1.2;
  }

  // 메인 텍스트 (채대원)
  &__main {
    font-weight: 700;
    font-size: 1.25rem;
    color: #1f2937;
  }

  // 서브 텍스트 (소프트)
  &__sub {
    font-weight: 500;
    font-size: 0.875rem;
    color: #6b7280;
    margin-top: -0.125rem;
  }

  // 크기별 스타일
  &--small {
    gap: 0.5rem;

    .app-logo__icon svg {
      width: 24px;
      height: 24px;
    }

    .app-logo__main {
      font-size: 1rem;
    }

    .app-logo__sub {
      font-size: 0.75rem;
    }
  }

  &--medium {
    gap: 0.75rem;

    .app-logo__icon svg {
      width: 32px;
      height: 32px;
    }

    .app-logo__main {
      font-size: 1.25rem;
    }

    .app-logo__sub {
      font-size: 0.875rem;
    }
  }

  &--large {
    gap: 1rem;

    .app-logo__icon svg {
      width: 40px;
      height: 40px;
    }

    .app-logo__main {
      font-size: 1.5rem;
    }

    .app-logo__sub {
      font-size: 1rem;
    }
  }

  // 반응형 디자인
  @media (max-width: 768px) {
    &:not(&--icon-only) {
      .app-logo__text {
        display: none;
      }
    }
  }
}
</style>