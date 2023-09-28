<template>
  <div class="redactor" ref="redactorElement">
    <div class="redactor__inner">
      <div class="redactor__buttons">
        <button class="redactor__button redactor__button-back" @click="undo"></button
        ><button class="redactor__button redactor__button-forward" @click="redo"></button
        ><button class="redactor__button redactor__button-title" @click="toTitle"></button
        ><button class="redactor__button redactor__button-paragraph" @click="toParagraph"></button
        ><button class="redactor__button redactor__button-image" @click="pasteImage"></button
        ><button class="redactor__button redactor__button-copy" @click="copyHTML">
          Скопировать HTML
        </button>
      </div>
      <p class="redactor__text" contenteditable="true">
        {{ redactorState.textBlock1 }}
      </p>
      <img class="redactor__image" :src="redactorState.imageSrc" alt="Redactor image" />
      <h1 class ="redactor__title" contenteditable="true">{{ redactorState.textTitle }}</h1>
      <p class="redactor__text" contenteditable="true">
        {{ redactorState.textBlock2 }}
      </p>
    </div>
  </div>
</template>
<script setup lang="ts">
import { reactive,ref } from "vue";
const redactorState = reactive({
  textTitle: `Смотрите какие обезьянки`,
  textBlock1: `Таким образом консультация с широким активом представляет собой
        интересный эксперимент проверки позиций, занимаемых участниками в
        отношении поставленных задач. С другой стороны постоянное
        информационно-пропагандистское обеспечение нашей деятельности
        представляет собой интересный эксперимент проверки форм развития.
        Идейные соображения высшего порядка, а также укрепление и развитие
        структуры влечет за собой процесс внедрения и модернизации
        соответствующий условий активизации. Задача организации, в особенности
        же реализация намеченных плановых заданий играет важную роль в
        формировании дальнейших направлений развития. Повседневная практика
        показывает, что постоянное информационно-пропагандистское обеспечение
        нашей деятельности играет важную роль в формировании существенных
        финансовых и административных условий.`,
  textBlock2: `        Таким образом консультация с широким активом представляет собой
        интересный эксперимент проверки позиций, занимаемых участниками в
        отношении поставленных задач. С другой стороны постоянное
        информационно-пропагандистское обеспечение нашей деятельности
        представляет собой инйцу шо шщйоц ущойц ущошцщйуо йцщуо йщцоу щйоу
        шщйцош ущйтересный эксперимент проверки форм развития. Идейные
        соображения высшего порядка, а также укрепление и развитие структуры
        влечет за собой процесс внедрения и модернизации соответствующий условий
        активизации. Задача организации, в особенности же реализация намеченных
        плановых заданий играет важную роль в формировании дальнейших
        направлений развития. Повседневная практика показывает, что постоянное
        информационно-пропагандистское обеспечение нашей деятельности играет
        важную роль в формировании существенных финансовых и административных
        условий. Товарищи! новая модель организационной деятельности требуют от
        нас анализа направлений прогрессивного развития. Задача организации, в
        особенности же постоянный количественный рост и сфера нашей активности
        требуют от нас анализа позиций, занимаемых участниками в отношении
        поставленных задач. Задача организации, в особенности же реализация
        намеченных плановых заданий требуют от нас анализа системы обучения
        кадров, соответствует насущным потребностям.`,

        imageSrc: "/monkeys-img.jpg"
});
const redactorElement = ref();

const copyHTML = async () => {
  try {
      await navigator.clipboard.writeText(redactorElement.value?.innerHTML)
      const text = await navigator.clipboard.readText()
      console.log("Copyed HTML:",text)
    } catch (err) {
      console.error('Failed to copy: ', err);
    }
}

const pasteImage = () => {
  const newUrl = prompt('Paste image URL','no')
  if(newUrl) document.execCommand('insertImage',false,newUrl)
}
const redo = () => {
  document.execCommand('redo', false)
}
const undo = () => {
  document.execCommand('undo', false)
}
const toTitle = () => {
document.execCommand('fontSize',false,'5')
}
const toParagraph = async () => {  
  document.execCommand('insertParagraph',false,)
}
</script>
<style scoped lang="scss">
.redactor {
  display: flex;
  justify-content: center;
  &__inner {
    max-width: 740px;

  }
  &__buttons {
    display: flex;
    align-items: center;
    column-gap: 12px;
    flex-wrap: wrap;
    margin-bottom: 31px;
  }
  &__button {
    width: 42px;
    height: 38px;
    color: #639eff;
    background-color: transparent;
    outline: none;
    border-style: none;
    &-back {
      background-image: url("../assets/back-icon.svg");
    }
    &-forward {
      background-image: url("../assets/forward-icon.svg");
    }
    &-title {
      background-image: url("../assets/title-icon.svg");
    }
    &-paragraph {
      background-image: url("../assets/paragraph-icon.svg");
    }
    &-image {
      background-image: url("../assets/image-icon.svg");
    }
    &-copy {
      width: auto;
      height: 24px;
    }
  }
  &__text {
    margin-bottom: 46px;
  }
  &__title {
    margin-bottom: 33px;
  }
  &__image {
    max-width: 100%;
    height: auto;
    margin-bottom: 31px;
  }
  &__textarea {
    width: 100%;
    color: #EAEAEA;;
    background-color: transparent;
    resize: none;
    overflow: hidden;
    height: auto;
    min-height: 100px;
  }
}
</style>
