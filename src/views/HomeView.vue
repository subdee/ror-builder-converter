<script setup>
import {ref} from "vue";
import oldAbilities from '@/json/old-ability-id-map.json';

let uri = ref('');
const convert = () => {
  const url = new URL(uri.value);
  const career = url.pathname.split('/')[2]
  const careerAbilities = oldAbilities[career]
  const convertedAbilities = {m1: [], m2: [], m3: [], m4: [], ma: [], mm: [], mt: [], t: []};
  ['m1', 'm2', 'm3', 'm4', 'ma', 'mm', 'mt', 't'].forEach(param => {
    const p = url.searchParams.get(param)
    p.split(',').forEach(a => {
      if (!a) {
        return
      }
      if (a in careerAbilities) {
        convertedAbilities[param].push(careerAbilities[a])
      } else {
        convertedAbilities[param].push(a)
      }
    })
  })

  const newParams = new URLSearchParams();
  newParams.set('l', url.searchParams.get('l'))
  newParams.set('r', url.searchParams.get('r'))
  newParams.set('tl', url.searchParams.get('tl'))
  newParams.set('mp', url.searchParams.get('mp'))
  newParams.set('pA', url.searchParams.get('pA'))
  newParams.set('pB', url.searchParams.get('pB'))
  newParams.set('pC', url.searchParams.get('pC'))
  for (const a in convertedAbilities) {
    newParams.set(a, convertedAbilities[a].join(','))
  }
  window.location = `${url.protocol}//${url.hostname}${url.pathname}?${newParams}`
}
</script>

<template>
  <main>
    <div class="field">
      <label class="label">Builder URL</label>
      <div class="control">
        <input class="input" type="text" v-model="uri" placeholder="Paste here the broken builder URL">
      </div>
    </div>
    <div class="field">
      <div class="control">
        <button class="button is-primary" @click="convert">Go to builder</button>
      </div>
    </div>
  </main>
</template>
