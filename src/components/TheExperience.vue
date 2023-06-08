<script setup lang="ts">
import { ref } from 'vue';
import { Color, SRGBColorSpace } from 'three';
import { STLLoader } from 'three/examples/jsm/loaders/STLLoader';

import { useLoader } from '@tresjs/core';
import { OrbitControls, GLTFModel } from '@tresjs/cientos';

const bgColor = new Color('#82DBC5');

const gl = {
  clearColor: '#82DBC5',
  outputColorSpace: SRGBColorSpace,
};

const meshPosition = [0, 3, 0];

const lightRef = ref(null);

const geometry = await useLoader(
  STLLoader,
  'https://raw.githubusercontent.com/Sea-DH1/examples/blob/master/public/assets/models/test.stl'
);

console.log(geometry);
</script>

<template>
  <Suspense>
    <TresCanvas v-bind="gl">
      <TresPerspectiveCamera :position="[9, 9, 9]" />
      <OrbitControls />
      <TresMesh v-bind="scene"> </TresMesh>
      <TresAxesHelper :args="[1]" />
      <TresDirectionalLight :position="[0, 2, 4]" :intensity="2" cast-shadow />
    </TresCanvas>
  </Suspense>
</template>
