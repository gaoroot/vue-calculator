<script setup>
import { ref } from 'vue'
import ButtonNumber from './components/ButtonNumber.vue'
import ButtonSymbol from './components/ButtonSymbol.vue'
import ButtonEqual from './components/ButtonEqual.vue'

const input = ref('')
const output = ref('')
const calculated = ref(false)

const clear = () => {
  input.value = ''
  output.value = ''
}

const cancel = () => {
  const arr = input.value.split('')
  arr.pop()
  input.value = arr.join('')
}

const enter = (keys) => {
  if (!calculated.value) {
    input.value += keys
  } else {
    calculated.value = false
    input.value = ''
    output.value = ''
    input.value += keys
  }
}

const equal = () => {
  if (input.value.includes('%')) {
    const arr = input.value.split('')
    const newArr = []
    for (let i of arr) {
      if (i !== '%') {
        newArr.push(i)
      } else {
        newArr.push('/100')
      }
    }
    input.value = newArr.join('')
  }
  output.value = eval(input.value)
  calculated.value = true
}
</script>

<template>
  <div class="flex flex-col items-center">
    <div class="flex flex-col gap-3 p-8 text-4xl">
      <div class="alert h-18">
        <span>{{ input || 0 }}</span>
      </div>
      <div class="alert h-18">
        <span>{{ output || 0 }}</span>
      </div>
    </div>
    <div class="flex gap-3 p-2">
      <ButtonSymbol @click="clear" symbol="CE" />
      <ButtonSymbol @click="cancel" symbol="C" />
      <ButtonSymbol @click="enter('%')" symbol="%" />
      <ButtonSymbol @click="enter('/')" symbol="/" />
    </div> 
    <div class="flex gap-3 p-2">
      <ButtonNumber @click="enter(7)" number="7" />
      <ButtonNumber @click="enter(8)" number="8" />
      <ButtonNumber @click="enter(9)" number="9" />
      <ButtonSymbol @click="enter('*')" symbol="x" />
    </div>
    <div class="flex gap-3 p-2">
      <ButtonNumber @click="enter(4)" number="4" />
      <ButtonNumber @click="enter(5)" number="5" />
      <ButtonNumber @click="enter(6)" number="6" />
      <ButtonSymbol @click="enter('-')" symbol="-" />
    </div>
    <div class="flex gap-3 p-2">
      <ButtonNumber @click="enter(1)" number="1" />
      <ButtonNumber @click="enter(2)" number="2" />
      <ButtonNumber @click="enter(3)" number="3" />
      <ButtonSymbol @click="enter('+')" symbol="+" />
    </div>
    <div class="flex gap-3 p-2">
      <ButtonSymbol @click="enter('.')" symbol="." />
      <ButtonNumber @click="enter(0)" number="0" />
      <ButtonEqual @click="equal" symbol="=" />
    </div>
  </div>
</template>
