<script lang="ts">
  import { SvelteSet } from 'svelte/reactivity'
  import { useStudio } from '../../internal/extensions'
  import {
    studioObjectsRegistryScope,
    type StudioObjectsRegistryActions,
    type StudioObjectsRegistryState
  } from './types'

  const { createExtension } = useStudio()

  createExtension<StudioObjectsRegistryState, StudioObjectsRegistryActions>({
    scope: studioObjectsRegistryScope,
    state() {
      return {
        objects: new SvelteSet()
      }
    },
    actions: {
      addObject({ state }, object) {
        state.objects.add(object)
      },
      removeObject({ state }, object) {
        state.objects.delete(object)
      }
    }
  })
</script>

<slot />
