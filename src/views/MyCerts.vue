<template>
  <Content>
    <PageTitle
      class="mb-6"
    >
      <template #right>
        <KButton
          data-testid="create-application-button"
          appearance="primary"
          :is-rounded="false"
          :to="{ name: 'create-application' }"
        >
          <svg
            width="16"
            height="16"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
            class="mr-2"
          >
            <title>My Certs</title>
            <path
              fill-rule="evenodd"
              clip-rule="evenodd"
              d="M16 8A8 8 0 110 8a8 8 0 0116 0zM7 5a1 1 0 012 0v2h2a1 1 0 110 2H9v2a1 1 0 11-2 0V9H5a1 1 0 110-2h2V5z"
              fill="#fff"
              fill-opacity=".75"
            />
          </svg>
          New Cert
        </KButton>
      </template>
    </PageTitle>
  </Content>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import usePortalApi from '@/hooks/usePortalApi'
import { useI18nStore } from '@/stores'

export default defineComponent({
  name: 'MyCerts',
  setup () {
    const { portalApiV2 } = usePortalApi()

    const logoSrc = portalApiV2.value.getApiLink('/api/v2/portal/logo')
    const helpText = useI18nStore().state.helpText.notFound

    return {
      logoSrc,
      helpText
    }
  }
})
</script>

<style lang="scss" scoped>
.not-found {
  --timingFunction: cubic-bezier(.785, .135, .15, .86);
  height: calc(100vh - var(--headerHeight));

  h1,
  .circle {
    opacity: 0;
    animation: .75s var(--timingFunction) forwards fadeIn;
  }

  h1 { animation-delay: 1.25s; }
  .circle { animation-delay: 1s; }

  .circle {
    padding: 3rem;
    margin: 4rem 0;
    font-size: 2.5rem;
    border-radius: 50%;
    border: 1px solid var(--section_colors-stroke);
  }

  .logo {
    max-height: 41px;
  }
}

</style>
