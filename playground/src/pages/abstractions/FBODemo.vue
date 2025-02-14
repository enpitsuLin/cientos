<script setup lang="ts">
import { TresCanvas, useRenderLoop } from '@tresjs/core'
import { OrbitControls, useTweakPane, Fbo } from '@tresjs/cientos'
import { SRGBColorSpace, ACESFilmicToneMapping } from 'three'

const gl = {
  clearColor: '#82DBC5',
  shadows: true,
  alpha: false,
  outputColorSpace: SRGBColorSpace,
  toneMapping: ACESFilmicToneMapping,
}

const fboRef = ref(null)
const materialRef = ref(null)
const torusRef = shallowRef(null)
const capsuleRef = shallowRef(null)

const { onLoop } = useRenderLoop()

const state = shallowReactive({
  depth: false,
  settings: {
    samples: 1,
  },
})

onMounted(async () => {
  await nextTick()

  onLoop(({ elapsed }) => {
    torusRef.value.rotation.x = elapsed * 0.745
    torusRef.value.rotation.y = elapsed * 0.361

    capsuleRef.value.rotation.x = elapsed * 0.471
    capsuleRef.value.rotation.z = elapsed * 0.632
  })

  setupTweakpane()
})

function setupTweakpane() {
  const { pane } = useTweakPane()

  pane.title = 'FBO config'

  pane.addInput(state, 'depth', { label: 'Toggle Depth Buffer' })

  pane.addInput(state.settings, 'samples', {
    label: 'MSAA Samples',
    min: 0,
    max: 8,
    step: 1,
  })
}
</script>

<template>
  <TresCanvas v-bind="gl">
    <TresPerspectiveCamera :position="[0, 0.5, 5]" />
    <OrbitControls />

    <TresGridHelper :args="[10, 10]" />

    <Fbo
      ref="fboRef"
      v-bind="state"
    />

    <TresMesh>
      <TresBoxGeometry :args="[1, 1, 1]" />
      <TresMeshBasicMaterial
        ref="materialRef"
        :color="0xff8833"
        :map="fboRef?.value.texture ?? null"
      />
    </TresMesh>

    <TresMesh
      ref="torusRef"
      :position="[3, 0, 0]"
    >
      <TresTorusGeometry :args="[1, 0.5, 16, 100]" />
      <TresMeshNormalMaterial />
    </TresMesh>

    <TresMesh
      ref="capsuleRef"
      :position="[-2, 0, 0]"
    >
      <TresCapsuleGeometry :args="[0.4, 1, 4, 8]" />
      <TresMeshNormalMaterial />
    </TresMesh>
  </TresCanvas>
</template>
