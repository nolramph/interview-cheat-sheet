<template>
    <div class="container">
      <div class="titles-panel">
        <ul :style="{'padding-bottom': titles.length * 5 + 'px'}">
          <li v-for="(item, index) in titles" :key="index" @click="selectTitle(index)">
           <span v-html="item.title"></span>
          </li>
        </ul>
      </div>
      <div class="content-panel">
        <div v-if="selectedTitle !== null">
          <h2 v-html="titles[selectedTitle].title"></h2>
          <p>{{ titles[selectedTitle].content }}</p>
        </div>
      </div>
    </div>
  </template>
  
  <script lang="ts">
  import { defineComponent, ref, onMounted } from 'vue';
  import {INTERVIEW_CONTENT} from '@/constants';
  import DOMPurify from 'dompurify';

  
  interface TitleContent {
    title: string;
    content: string;
  }
  
  export default defineComponent({
    name: 'TitleContentDisplay',
    setup() {
  
      const selectedTitle = ref<number | null>(0);
      const titles = ref<TitleContent[]>(INTERVIEW_CONTENT);
  
      function selectTitle(index: number): void {
        selectedTitle.value = index;
      }

    onMounted(() => {
        titles.value = INTERVIEW_CONTENT.map(item => ({
        title: DOMPurify.sanitize(item.title),
        content: item.content, // Assuming content does not need HTML and thus not sanitized for this example
      }));
    });
  
      return { titles, selectedTitle, selectTitle };
    },
  });
  </script>
  
  <style>
  .container {
    display: flex;
    text-align: left;
    height: calc(100vh - 50px); 
    width: 100vw;
    overflow: hidden;
  }
  
  .titles-panel {
    flex: 1;
    border-right: 1px solid #ccc;
    overflow-y: auto;
    scrollbar-width: thin;
    scrollbar-color: #888 #f0f0f0;   
}

  .titles-panel::-webkit-scrollbar {
    width: 8px;
  }

  .titles-panel::-webkit-scrollbar-track {
    background: #f0f0f0;
  }

  .titles-panel::-webkit-scrollbar-thumb {
    background-color: #888;
    border-radius: 4px;
  }
  
  .content-panel {
    flex: 2;
    padding: 0 1rem;
    overflow-y: auto;
    line-height: 1.5;
  }

  .content-panel h2{
    font-weight: 400;
  }
  
  
  li {
    cursor: pointer;
    list-style: none;
    padding: 1rem;
    margin: 2px 0;
    overflow: hidden;
  }
  </style>
  