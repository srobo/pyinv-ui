<template>
  <page-layout :title="asset.display_name">
    <template #breadcrumbs><asset-breadcrumbs :asset="asset" /></template>
    <template #content>
      <asset-info :asset="asset" />
      <b-tabs>
        <b-tab-item label="Timeline">
          <timeline :asset="asset" />
        </b-tab-item>
      </b-tabs>
    </template>
  </page-layout>
</template>

<script>
export default {
  head() {
    return {
      title: `${this.asset.display_name} | PyInv`,
    }
  },
  async asyncData({ $axios, params, redirect }) {
    const asset = await $axios.$get('assets/' + params.uuid)
    if (asset.node && asset.node.numchild != 0) {
      redirect({ name: 'nodes-uuid', params: { uuid: asset.node.id } })
    }
    return { asset }
  },
}
</script>
