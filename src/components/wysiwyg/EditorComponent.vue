<template>
  <div>
    <control-component
      @undo="handleUndo"
      @redo="handleRedo"
      @convert-elements-to-tag="handleConvertElementsToTag"
      @insert-image="handleInsertImage"
      @copy-html="handleCopyHTML"
    />
    <div ref="editor" contenteditable="true" class="editor">
      <p v-html="content" />
    </div>
  </div>
</template>

<script>
import ControlComponent from './ControlComponent.vue';

export default {
  name: 'EditorComponent',
  components: {
    ControlComponent
  },
  data() {
    return {
      history: [],
      currentHistoryIndex: 0,
      editor: null,
      selectedElements: [],
      content: `
        <p class="editor__content-paragraph">Таким образом консультация с широким активом представляет собой интересный эксперимент проверки позиций, занимаемых участниками в отношении поставленных задач. С другой стороны постоянное информационно-пропагандистское обеспечение нашей деятельности представляет собой интересный эксперимент проверки форм развития. Идейные соображения высшего порядка, а также укрепление и развитие структуры влечет за собой процесс внедрения и модернизации соответствующий условий активизации. Задача организации, в особенности же реализация намеченных плановых заданий играет важную роль в формировании дальнейших направлений развития. Повседневная практика показывает, что постоянное информационно-пропагандистское обеспечение нашей деятельности играет важную роль в формировании существенных финансовых и административных условий.</p>
        <h2 class="editor__content-header">Смотрите какие обезьянки</h2>
        <p class="editor__content-paragraph"><img class="editor__content-image" src="https://i.postimg.cc/1R6882QW/monkeys.jpg" alt="Sample Image"></p>
        <p class="editor__content-paragraph">Таким образом консультация с широким активом представляет собой интересный эксперимент проверки позиций, занимаемых участниками в отношении поставленных задач. С другой стороны постоянное информационно-пропагандистское обеспечение нашей деятельности представляет собой инйцу шо шщйоц ущойц ущошцщйуо йцщуо йщцоу щйоу шщйцош ущйтересный эксперимент проверки форм развития. Идейные соображения высшего порядка, а также укрепление и развитие структуры влечет за собой процесс внедрения и модернизации соответствующий условий активизации. Задача организации, в особенности же реализация намеченных плановых заданий играет важную роль в формировании дальнейших направлений развития. Повседневная практика показывает, что постоянное информационно-пропагандистское обеспечение нашей деятельности играет важную роль в формировании существенных финансовых и административных условий.</p>
        <p class="editor__content-paragraph">Товарищи! новая модель организационной деятельности требуют от нас анализа направлений прогрессивного развития. Задача организации, в особенности же постоянный количественный рост и сфера нашей активности требуют от нас анализа позиций, занимаемых участниками в отношении поставленных задач. Задача организации, в особенности же реализация намеченных плановых заданий требуют от нас анализа системы обучения кадров, соответствует насущным потребностям.</p>
      `,
    };
  },
  computed: {
    canUndo() {
      return this.currentHistoryIndex >= 0
    },
    canRedo() {
      return this.currentHistoryIndex < this.history.length - 1
    }
  },
  mounted() {
    this.init()
  },
  methods: {
    init() {
      this.editor = this.$refs.editor;
      this.editor.innerHTML = this.content;
      this.editor.focus();
      window.addEventListener('mouseup', this.handleSelection);
      window.addEventListener('input', this.updateContent);
      this.updateContent();
    },
    handleConvertElementsToTag(elementTag) {
      if (this.selectedElements && this.selectedElements.length > 0) {
        this.selectedElements.forEach((element) => {
          const newElement = document.createElement(elementTag);
          newElement.className = elementTag === 'p' ? 'editor__content-paragraph' : 'editor__content-header';
          newElement.innerHTML = element.innerHTML;
          element.parentNode.replaceChild(newElement, element);
        });

        this.updateContent();
        this.selectedElements = null;
      }
    },
    async handleInsertImage() {
      const imageUrl = prompt('Введите URL:');
      if (imageUrl) {
        await this.loadImage(imageUrl);
        this.updateContent();
      }
    },
    async handleCopyHTML() {
      const selection = window.getSelection();

      if (!selection.isCollapsed) {
        const tempContainer = document.createElement('div');

        for (let i = 0; i < selection.rangeCount; i++) {
          const range = selection.getRangeAt(i).cloneContents();
          tempContainer.appendChild(range);
        }
        const contentToCopy = tempContainer.innerHTML;

        try {
          await navigator.clipboard.writeText(contentToCopy);
          window.alert('Выделенный HTML скопирован')
        } catch (err) {
          window.alert(`Невозможно скопировать выделенный HTML. Ошибка: ${err.message}`)
        }
      }
    },
    handleUndo() {
      if (this.canUndo) {
        this.currentHistoryIndex -= 1;
        this.updateEditorContent();
      }
    },
    handleRedo() {
      if (this.canRedo) {
        this.currentHistoryIndex += 1;
        this.updateEditorContent();
      }
    },
    async loadImage(url) {
      return new Promise((resolve, reject) => {
        const image = new Image();
        image.className = 'editor__content-image';
        image.onload = () => {
          this.editor.focus();
          const range = window.getSelection().getRangeAt(0);
          range.insertNode(image);
          resolve();
        };
        image.onerror = () => {
          reject(new Error(window.alert('Введен неправильный URL изображения')));
        };
        image.src = url;
      });
    },
    updateContent() {
      const newContent = this.editor.innerHTML;
      if (newContent !== this.content) {
        this.history.splice(this.currentHistoryIndex + 1);
        this.history.push(newContent);
        this.currentHistoryIndex += 1;
        this.content = newContent;
      }
    },
    updateEditorContent() {
      this.editor.innerHTML = this.history[this.currentHistoryIndex] || this.content;
    },
    getElementsInRange(range) {
      const elements = [];
      const walker = document
        .createTreeWalker(range.commonAncestorContainer, NodeFilter.SHOW_ELEMENT);

      while (walker.nextNode()) {
        const node = walker.currentNode;
        if (range.intersectsNode(node)) {
          elements.push(node);
        }
      }
      return elements;
    },
    handleSelection() {
      const selection = document.getSelection();

      if (selection.isCollapsed) {
        return;
      }

      const selectedElements = [];

      for (let i = 0; i < selection.rangeCount; i++) {
        const range = selection.getRangeAt(i);
        const elementsInRange = this.getElementsInRange(range);

        selectedElements.push(...elementsInRange);
      }

      this.selectedElements = selectedElements.filter(
        (element) => element.tagName.toLowerCase() !== 'img'
      );

      if (!this.selectedElements.length) {
        for (let i = 0; i < selection.rangeCount; i++) {
          const range = selection.getRangeAt(i);
          const parentElement = range.commonAncestorContainer.nodeType === Node.ELEMENT_NODE
            ? range.commonAncestorContainer
            : range.commonAncestorContainer.parentNode;

          if (parentElement.nodeType === Node.ELEMENT_NODE) {
            this.selectedElements.push(parentElement);
          }
        }
      }
    },
  },
};
</script>

<style>
.editor{
  padding: 4px;
  padding: clamp(.06rem, .41vw, .25rem);
}

.editor__content-paragraph {
  margin-bottom: clamp( .5rem, 1.875vw, 1.125rem);
}

.editor__content-header {
  font-size: clamp(1rem, 3.229vw, 1.9375rem);
  font-weight: 400;
  color: var(--color-heading);
  margin-bottom: clamp( .5625rem, 1.9792vw, 1.1875rem);
}

.editor__content-image {
  max-width: 739px;
  width: 100%;
  border-radius: 10px;
  object-fit: cover;
}
</style>
