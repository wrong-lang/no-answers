<script setup>
import {onMounted, ref} from "vue";

let timeInitial = new Date().getTime()
let isAnswer = ref(false)
let back = ref( Math.trunc((Math.trunc(Math.random() * 100)) ** 6 + Math.sin(Math.random() * 100) * 1000))

onMounted(() => {
  function time() {
    if (isAnswer.value && back.value > 0) {
      back.value -= 1
    }
    window.requestAnimationFrame(time);
  }
  window.requestAnimationFrame(time);

  document.getElementById("b").addEventListener("click", () => {
    if (back.value <= 0) {
      isAnswer.value = false
      back.value = Math.trunc((Math.trunc(Math.random() * 1000)) ** 6 + Math.sin(Math.random() * 100) * 1000)
    } else {
      alert("มึงก็รีบเกิ๊น")
    }
  })
})

function getAnswer() {
  let timeFinal = new Date().getTime()
  if (timeFinal - timeInitial < 3000) {
    isAnswer.value = true
  } else {
    alert("มึงคิดนานเกิ๊น")
  }
  timeInitial = new Date().getTime()
}

</script>

<template>
  <center class="absolute top-2 w-full text-white">
    <a href="https://tinarskii.com">Website of <span class="underline">Tinarskii</span></a>
  </center>
  <div class="grid grid-cols-1 gap-8 min-h-screen place-items-center">
    <div v-show="!isAnswer" class="flex flex-col md:col-span-2 gap-16 w-full items-center">
      <div class="flex flex-col gap-2">
        <h1 class="font-black text-white sm:text-6xl text-5xl text-center">
          เว็บนี้ไม่มีคำตอบ
        </h1>
        <p class="font-extrabold text-slate-400 italic text-center">
          The Web without Answers
        </p>
      </div>
      <div class="flex flex-col gap-6">
        <div class="mx-auto bg-black/80 rounded-lg p-1">
          <h1 class="text-orange-500 text-2xl p-2 rounded-lg text-center">
            วิธีไม่ใช้
          </h1>
        </div>
        <ol class="text-white">
          <li>ไม่ต้องตั้งคำถามแบบปลายปิดในใจ เช่น วันนี้ไม่ต้องทำอะไร หรือ เย็นนี้ไม่อยากกินอะไร</li>
          <li>ไม่ต้องมีสมาธิและสติประมาณ 10 ถึง 15 มิลลิวินาที</li>
          <li>กดที่ปุ่มเพื่อไม่ต้องรับคำตอบ</li>
        </ol>
      </div>
      <button class="bg-black/50 text-white text-xl px-8 py-4 rounded-lg" v-on:click="getAnswer()">
        กดเพื่อไม่ได้รับคำตอบ
      </button>
    </div>
    <div v-show="isAnswer" class="flex flex-col gap-12 items-center justify-center">
      <h1 class="font-black text-white sm:text-9xl text-7xl text-center animate-[drop_8s_forwards]">
        ไม่รู้
      </h1>
      <button class="bg-black/50 text-white text-xl px-8 py-4 rounded-lg" id="b">
        กลับหน้าแรกภายใน {{ back }} เฟรม
      </button>

    </div>
  </div>
</template>
