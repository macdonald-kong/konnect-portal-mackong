<template>
  <Content>

    <header class="mb-6">
      <h1 class="m-0 type-xl color-text_colors-headings">My Certs</h1>
    </header>

    <KCard title="Manage Certificates">
      <template v-slot:body>
        <KTable :fetcher="fetcher" :headers="headers" :hasSideBorder="true" />
      </template>
    </KCard>
    
    <br/>
    
    <KCard title="Add New Certificate">
      <template v-slot:body>
        <p>Please enter your certificates details:</p>
        <br/>
        <form action="https://localhost:8443/consumers" method="post" target="_blank">
          <KLabel for="uname">Username:</KLabel>
          <KInput id="uname" name="uname"/>
          <KLabel for="cn">Common Name:</KLabel>
          <KInput id="cn" name="cn"/>
          <br/>
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
  setup() {
    const { portalApiV2 } = usePortalApi()

    const logoSrc = portalApiV2.value.getApiLink('/api/v2/portal/logo')
    const helpText = useI18nStore().state.helpText.notFound

    const headers = [
      { label: 'ID', key: 'id', sortable: true },
      { label: 'CN', key: 'cn', sortable: true }
    ]

    const sortHandlerFn = ({ key, sortColumnOrder, data }) => {
      return data.sort((a, b) => {
        if (key === 'last_seen') {
          if (sortColumnOrder === 'asc') {
            if (a.last_ping > b.last_ping) {
              return 1
            } else if (a.last_ping < b.last_ping) {
              return -1
            }
            return 0
          } else {
            if (a.last_ping > b.last_ping) {
              return -1
            } else if (a.last_ping < b.last_ping) {
              return 1
            }
            return 0
          }
        }
      })
    }

    const fetcher = () => {
      return {
        data: [
          {
            id: '08cc7d81-a9d8-4ae1-a42f-8d4e5a919d07',
            cn: 'demo-cn',
          },
          {
            id: '08cc7d81-a9d8-4ae1-a42f-8d4e5a919d07',
            cn: 'example-cn',
          },
        ]
      }
    }

    return {
      logoSrc,
      helpText,
      headers,
      sortHandlerFn,
      fetcher
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
