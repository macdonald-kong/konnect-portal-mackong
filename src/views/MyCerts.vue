<template>
  <Content>

    <header class="mb-6">
      <h1 class="m-0 type-xl color-text_colors-headings">My Certs</h1>
    </header>

    <p>Please enter the CN from your certificate:</p>

    <form action="http://localhost:8000/consumers" method="post" target="_blank">
      <label for="uname">Username:</label>
      <input type="text" id="uname" name="uname"><br><br>
      <label for="cn">Common Name:</label>
      <input type="text" id="cn" name="cn"><br><br>
      <input type="submit" value="Submit">
    </form>

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
