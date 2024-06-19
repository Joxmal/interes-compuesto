<template>
  <div v-if="$props.dias > 0 || $props.monto > 0" class="w-full  flex flex-col  max-w-sm p-4 bg-white border border-gray-200 rounded-lg shadow dark:bg-gray-800 dark:border-gray-700 dark:text-white">
    <h5 class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white">Calculadora de ganancias</h5>

    <div v-for="(item, index) in dias_monto_acumulado" :key="index" class="flex flex-row justify-between mb-2" >
      <div class="text-gray-700 dark:text-gray-400" > Dia {{ item.dia }} </div>
      <div class="text-gray-700 dark:text-gray-400" > {{ item.monto.toFixed(2) }}$</div>
    </div>
      
  </div>
</template>

<script setup lang="ts">
import { ref, Ref, watch } from 'vue';



const dias_monto_acumulado: Ref<Array<{ dia: number; monto: number }>> = ref([])



interface Props {
  dias: number
  monto: number
}

const props = defineProps<Props>()

function calcular_ganancia({dias, monto}:{dias:number, monto:number}) {
  if (dias <= 0 || monto <= 0) return

  console.log(`Monto inicial: ${monto}$`)
    dias_monto_acumulado.value.push({ dia: 0, monto })
  let ganancia_total = monto;
  for (let index = 0; index < dias; index++) {

    if(ganancia_total < 54){
      ganancia_total += (ganancia_total * 0.14)- ((ganancia_total*0.14)*0.02);
      console.log(`dia ${index + 1}: ${ganancia_total.toFixed(2)}$ `);

    }else{
      ganancia_total += (ganancia_total * 0.143)- ((ganancia_total*0.143)*0.02);
      console.log(`dia ${index + 1}: ${ganancia_total.toFixed(2)}$ `);
    }



    
    dias_monto_acumulado.value.push({ dia: index + 1, monto: ganancia_total })
  }
}

calcular_ganancia({dias:props.dias,monto:props.monto})

watch(() => props.dias, (newValue, oldValue) => {
  console.log(`dias cambio de ${oldValue} a ${newValue}`)
  dias_monto_acumulado.value = []
  calcular_ganancia({dias:props.dias,monto:props.monto})
})

watch(() => props.monto, (newValue, oldValue) => {
  console.log(`Monto cambio de ${oldValue} a ${newValue}`)
  dias_monto_acumulado.value = []
  calcular_ganancia({dias:props.dias,monto:props.monto})
})

watch



</script>