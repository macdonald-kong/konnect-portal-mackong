<template>
  <Content>

  <KCard title="Manage Certificates">
    <template v-slot:body>
      I am the body.
    </template>
  </KCard>

  <KCard title="Add New Certificate">
    <template v-slot:body>
      <p>Please enter your certificates details:</p>
      <form action="https://localhost:8443/consumers" method="post" target="_blank">
        <KLabel for="uname">Username:</KLabel>
        <KInput id="uname" name="uname"/>
        <KLabel for="cn">Common Name:</KLabel>
        <KInput id="cn" name="cn"/>
        <KButton appearance="primary" type="submit">Submit</KButton>
      </form>
    </template>
  </KCard>



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
