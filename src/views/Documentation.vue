<template>
  <Content>
    <header class="mb-6">
      <h1 class="m-0 type-xl color-text_colors-headings">Documentation</h1>
    </header>
    <KTabs :tabs="tabs">
      <template v-slot:tab1>
        <header class="mb-6 mt-4">
          <h1 class="m-0 type-xl color-text_colors-headings">Authorization</h1>
        </header>
        <p>The authorization server exposes Openid-configuration (well known configuration) which provides configuration information about the Identity provider (IDP).</p>
        <p>Read more about Openid-configuration here.</p>
        <p>Íslandsbanki's Openid-configuration</p>
      </template>
      <template v-slot:tab2>
        <header class="mb-6 mt-4">
          <h1 class="m-0 type-xl color-text_colors-headings">Cards API Guide</h1>
        </header>
        <p>This guide explains how to consume the Cards API with OAuth2 authorization flow.</p>
      </template>
      <template v-slot:tab3>
        <header class="mb-6 mt-4">
          <h1 class="m-0 type-xl color-text_colors-headings">Accounts API guide</h1>
        </header>
        <p>This guide explains how to consume the Accounts API with OAuth2 authorization flow.</p>
      </template>
      <template v-slot:tab4>
        <header class="mb-6 mt-4">
          <h1 class="m-0 type-xl color-text_colors-headings">Payments API guide</h1>
        </header>
        <p>This guide explains how to initiate payment.</p>
      </template>
      <template v-slot:tab5>
        <header class="mb-6 mt-4">
          <h1 class="m-0 type-xl color-text_colors-headings">Test data for sandbox environment</h1>
        </header>
        <p>The following test data is available for sandbox interaction.</p>
      </template>
    </KTabs>
  </Content>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import usePortalApi from '@/hooks/usePortalApi'
import { useI18nStore } from '@/stores'

export default defineComponent({
  name: 'Documentation',
  setup () {
    const { portalApiV2 } = usePortalApi()

    const logoSrc = portalApiV2.value.getApiLink('/api/v2/portal/logo')
    const helpText = useI18nStore().state.helpText.notFound
    const tabs = [
      {
        hash: '#tab1',
        title: 'Authorization'
      },
      {
        hash: '#tab2',
        title: 'Cards'
      },
      {
        hash: '#tab3',
        title: 'Accounts'
      },
      {
        hash: '#tab4',
        title: 'Payments'
      },
      {
        hash: '#tab5',
        title: 'Test Data'
      }
    ]

    return {
      logoSrc,
      helpText,
      tabs
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
