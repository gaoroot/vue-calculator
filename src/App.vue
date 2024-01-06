<script setup>
import { ref } from 'vue'
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
      <div class="btn btn-outline btn-warning size-16 text-3xl" @click="clear">CE</div>
      <div class="btn btn-outline btn-warning size-16 text-3xl" @click="cancel">&larr;</div>
      <div class="btn btn-outline btn-warning size-16 text-3xl" @click="enter('%')">%</div>
      <div class="btn btn-outline btn-warning size-16 text-3xl" @click="enter('/')">/</div>
    </div> 
    <div class="flex gap-3 p-2">
      <div class="btn size-16 text-3xl" @click="enter(7)">7</div>
      <div class="btn size-16 text-3xl" @click="enter(8)">8</div>
      <div class="btn size-16 text-3xl" @click="enter(9)">9</div>
      <div class="btn btn-outline btn-warning size-16 text-3xl" @click="enter('*')">*</div>
    </div>
    <div class="flex gap-3 p-2">
      <div class="btn size-16 text-3xl" @click="enter(4)">4</div>
      <div class="btn size-16 text-3xl" @click="enter(5)">5</div>
      <div class="btn size-16 text-3xl" @click="enter(6)">6</div>
      <div class="btn btn-outline btn-warning size-16 text-3xl" @click="enter('-')">-</div>
    </div>
    <div class="flex gap-3 p-2">
      <div class="btn size-16 text-3xl" @click="enter(1)">1</div>
      <div class="btn size-16 text-3xl" @click="enter(2)">2</div>
      <div class="btn size-16 text-3xl" @click="enter(3)">3</div>
      <div class="btn btn-outline btn-warning size-16 text-3xl" @click="enter('+')">+</div>
    </div>
    <div class="flex gap-3 p-2">
      <div class="btn size-16 text-3xl" @click="enter(0)">0</div>
      <div class="btn size-16 text-3xl" @click="enter('.')">.</div>
      <div class="btn btn-outline btn-warning size-16 w-36 text-3xl" @click="equal">=</div>
    </div>
  </div>
</template>
