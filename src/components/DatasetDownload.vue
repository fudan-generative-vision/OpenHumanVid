<template>
    <section class="dataset-download">
      <div>
        <h2 class="title">{{ title }}</h2>


        <div class="download-section">
          <div v-for="(item, index) in datasets" :key="index" class="download-item">
            <button class="download-button" @click="handleDownload">
              {{ item.name }}
            </button>

            <span class="download-details">{{ item.details }}</span>
          </div>
        </div>

        <div v-if="updates" class="update-section">
          <h3>🔥 Warning ({{ updates.date }})</h3>
          <p>
            {{ updates.notes }}
            <a :href="updates.links.license">Our license</a>.
          </p>
          <p>
            {{ updates.description }}
            <a :href="updates.links.details">Fill out the form</a>.
          </p>
        </div>
        
      </div>
    </section>
  </template>
  
  <script setup lang="ts">
  interface Dataset {
    name: string;
    details: string;
  }
  
  interface Updates {
    date: string;
    description: string;
    links: {
      details: string;
      license: string;
    };
    notes: string;
  }
  
  interface Props {
    title?: string;
    datasets?: Dataset[];
    updates?: Updates;
  }
  
  const { props } = defineProps<{ props: Props }>();
  const title = props.title || "Dataset Download";
  const datasets = props.datasets || [];
  const updates = props.updates || null;

  const handleDownload = () => {
    window.location.href = 'https://forms.gle/moqec5Qod7mz9pfD6';
  };
  </script>
  
  <style lang="scss" scoped>
  .dataset-download {
    text-align: center; /* Ensures entire section is centered */
  
    .title {
      margin-bottom: 80px;
    //   font-family: 'Caveat', cursive;
    //   font-size: 2.5rem;
      margin: 5;
    }

    .update-section {
      margin-top: 30px;
      text-align: left;
      padding: 20px;
      background-color: #f9f9f9;
      border: 1px solid #ccc;
      border-radius: 5px;
      max-width: 1400px;
  
      h3 {
        color: #e63946;
      }
  
      a {
        color: #007BFF;
        text-decoration: none;
        font-size: 16px;
  
        &:hover {
          text-decoration: underline;
        }
      }
    }
  
    .download-section {
      display: flex;
      flex-direction: column;
      align-items: center;
      max-width: 1400px;
    }
  
    .download-item {
      margin-bottom: 15px;
      display: flex;
      align-items: center;
      justify-content: center;
      max-width: 1200px;
  
      .download-button {
        font-size: 24px;
        padding: 10px 20px;
        margin-right: 10px;
        background-color: #333;
        color: #fff;
        border: none;
        cursor: pointer;
  
        &:hover {
          background-color: #555;
        }
      }
  
      .download-details {
        font-size: 24px;
        color: #333;
      }

    }
  
    
  }
  </style>
  