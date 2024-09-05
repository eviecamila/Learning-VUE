<template>
  <div id="app">
    <header class="bg-blue-600 text-white py-4 text-center">
      <h1 class="text-2xl font-bold">Eventos Históricos de IA</h1>
    </header>

    <main class="container mx-auto p-6">
      <h2 class="text-xl font-semibold mb-4">Línea de tiempo de eventos:</h2>

      <!-- Lista de eventos -->
      <div id="eventsList" class="grid gap-6">
        <div v-for="event in events" :key="event.id"
          class="border rounded-lg p-4 cursor-pointer hover:bg-gray-100 transition" @click="openModal(event)">
          <h3 class="text-lg font-bold">{{ event.title }}</h3>
          <p class="text-gray-600">{{ event.description }}...</p>
        </div>
      </div>
    </main>

    <!-- Modal de evento -->
    <EventModal v-if="isModalVisible" :event="selectedEvent" @close="closeModal" />

    <!-- Modal de autor -->
    <GenericModal v-if="isAuthorModalVisible" @close="closeAuthorModal" @click="closeAuthorModal">
      <div style="padding-bottom: 10;display: grid;place-items: center;"><img src="/assets/me.webp" alt="Myself esa"
          width="50%"></div>
      <h2 class="text-black text-xl font-bold mb-4">Esta Timeline fue creada por La Evie.</h2>
      <p class="text-gray-700">Todo literal gracias a la AI! <br>
        Tengo que cuidar a mi Vue Developer (mi Ksimerito), Esta aprendiendo la tecno apenas.</p>
    </GenericModal>
  </div>
</template>

<script lang="ts">
import EventModal from './components/EventModal.vue';
import GenericModal from './components/Modal.vue';

export default {
  components: {
    EventModal,
    GenericModal
  },
  data() {
    return {
      isModalVisible: false,
      isAuthorModalVisible: true, // Mostrar el modal de autor al inicio
      selectedEvent: {} as any, // Asegúrate de que `selectedEvent` esté tipado correctamente
      events: [
        {
          "id": 1,
          "title": "1943-1955: Genesis IA",
          "description": "Investigadores como Alan Turing, John McCarthy y Marvin Minsky publican los primeros trabajos sobre sistemas de razonamiento artificial.",
          "images": [
            { "image": "/assets/genesis-ia-1.jpg", "quoted": "Mi apa el turing 🏳️‍🌈", "index": 1 },
            { "image": "/assets/genesis-ia-2.png", "quoted": "Prueba de turing", "index": 2 },
            { "image": "/assets/genesis-ia-3.webp", "quoted": "Razonamiento artificial", "index": 3 }
          ],
          "details": "En este período, Alan Turing propone el concepto de la 'máquina universal', un precursor de la computadora moderna, y su famoso test para evaluar la inteligencia de las máquinas. John McCarthy acuña el término 'Inteligencia Artificial' en la Conferencia de Dartmouth en 1956, que marca el inicio formal del campo."
        },
        {
          "id": 2,
          "title": "1956: Nacimiento AI",
          "description": "Se acuña el término 'Inteligencia Artificial' en la conferencia de Dartmouth College.",
          "images": [
            { "image": "/assets/nacimiento-ai-1.jpg", "quoted": "Dartmouth College", "index": 1 },
            { "image": "/assets/nacimiento-ai-2.webp", "quoted": "Conferencia de DM C", "index": 2 },
            { "image": "/assets/nacimiento-ai-3.jpeg", "quoted": "AI Drawing", "index": 3 }
          ],
          "details": "La Conferencia de Dartmouth de 1956 es ampliamente considerada como el evento fundador del campo de la inteligencia artificial. John McCarthy, Marvin Minsky, Nathaniel Rochester y Claude Shannon propusieron un proyecto de investigación de verano para explorar si las 'cualidades inteligentes' podrían ser descritas de manera precisa y simuladas por máquinas."
        },
        {
          "id": 3,
          "title": "1952-1969: Entusiasmo Inicial, Grandes esperanzas",
          "description": "Auge de los sistemas expertos basados en reglas.",
          "images": [
            { "image": "/assets/entusiasmo-inicial-1.png", "quoted": "Logic Theorist", "index": 1 },
            { "image": "/assets/entusiasmo-inicial-2.png", "quoted": "General Problem Solver", "index": 2 },
            { "image": "/assets/entusiasmo-inicial-3.jpg", "quoted": "", "index": 3 }
          ],
          "details": "Durante este período, se desarrollan los primeros programas de IA, como el 'Logic Theorist' de Allen Newell y Herbert A. Simon, y el 'General Problem Solver'. Estos sistemas se basan en la manipulación de símbolos y reglas para resolver problemas, marcando el inicio de los sistemas expertos."
        },
        {
          "id": 4,
          "title": "1966-1973: Una dosis de realidad",
          "description": "Decepción por la lenta evolución de la IA y recortes de financiación.",
          "images": [
            { "image": "/assets/dosis-de-realidad-1.jpeg", "quoted": "Invierno de la IA", "index": 1 },
            { "image": "/assets/dosis-de-realidad-2.jpeg", "quoted": "Lenta Evolución", "index": 2 },
            { "image": "/assets/dosis-de-realidad-3.jpg", "quoted": "Bajo financiamiento hacia el avance de la IA", "index": 3 }
          ],
          "details": "Este período es conocido por el primer 'invierno de la IA', una desaceleración en el progreso de la investigación en IA debido a expectativas no cumplidas y la falta de avances significativos. Los recortes en la financiación se deben a la desilusión con la capacidad de las máquinas para realizar tareas inteligentes."
        },
        {
          "id": 5,
          "title": "1969-1979: Sistemas basados en el conocimiento",
          "description": "Auge de los sistemas expertos basados en reglas.",
          "images": [
            { "image": "/assets/sistemas-conocimiento-1.jpeg", "quoted": "DENDRAL", "index": 1 },
            { "image": "/assets/sistemas-conocimiento-2.webp", "quoted": "Sistemas Basados en Reglas", "index": 2 },
            { "image": "/assets/sistemas-conocimiento-3.jpg", "quoted": "MYCIN, utilizado para el area medicinal", "index": 3 }
          ],
          "details": "Durante esta década, se desarrollan los sistemas expertos como DENDRAL y MYCIN, que utilizan bases de conocimiento y reglas de inferencia para resolver problemas en áreas específicas como la química y la medicina. Estos sistemas demostraron que la IA podía ser útil en aplicaciones prácticas."
        },
        {
          "id": 6,
          "title": "1980-actual: La AI se convierte en industria",
          "description": "Aplicaciones de IA en áreas como conducción autónoma, asistentes virtuales y diagnóstico médico.",
          "images": [
            { "image": "/assets/ai-industria-1.webp", "quoted": "La AI se vuelve una industria", "index": 1 },
            { "image": "/assets/ai-industria-2.png", "quoted": "Lenguaje natural", "index": 2 },
            { "image": "/assets/ai-industria-3.jpg", "quoted": "Asistentes virtuales modernos", "index": 3 }
          ],
          "details": "Desde los años 80, la IA se ha convertido en una industria en expansión, con avances en aprendizaje automático, procesamiento del lenguaje natural y visión por computadora. Las aplicaciones incluyen vehículos autónomos, asistentes virtuales como Siri y Alexa, y herramientas de diagnóstico en medicina como IBM Watson."
        },
        {
          "id": 7,
          "title": "1986-actual: Regreso a las redes neuronales",
          "description": "Resurgimiento del interés en las redes neuronales y el aprendizaje profundo.",
          "images": [
            { "image": "/assets/redes-neuronales-1.avif", "quoted": "Estructura de Redes Neuronales", "index": 1 },
            { "image": "/assets/redes-neuronales-2.jpg", "quoted": "BERT, el algoritmo de busqueda de Google", "index": 2 },
            { "image": "/assets/redes-neuronales-3.jpg", "quoted": "GPT, el modelo de lenguaje que soluciona todo", "index": 3 }
          ],
          "details": "El renacimiento del interés en las redes neuronales se debe a los avances en la capacidad computacional y el desarrollo de algoritmos de aprendizaje profundo. La red neuronal convolucional (CNN) de Yann LeCun para reconocimiento de dígitos manuscritos en los 80 y los modelos de Transformers como BERT y GPT han marcado una nueva era en la IA."
        },
        {
          "id": 8,
          "title": "1987-actual: La AI se convierte en una ciencia",
          "description": "La IA se establece como una disciplina académica con programas de investigación y desarrollo.",
          "images": [
            { "image": "/assets/ai-ciencia-1.jpeg", "quoted": "Uso de la IA en herramientas de edicion genomica", "index": 1 },
            { "image": "/assets/ai-ciencia-2.jpg", "quoted": "La neurociencia se desarrolla gracias a la IA", "index": 2 },
          ],
          "details": "La IA se consolida como una disciplina académica con la creación de programas de investigación en universidades y centros de investigación. Se desarrollan nuevas teorías y metodologías, y la IA comienza a colaborar con otras áreas de la ciencia, como la neurociencia y la biología."
        },
        {
          "id": 9,
          "title": "1995-actual: Emergencia de los sistemas inteligentes",
          "description": "Desarrollo de sistemas inteligentes en áreas como robótica, visión artificial.",
          "images": [
            { "image": "/assets/sistemas-inteligentes-1.jpg", "quoted": "Robot humanoide autonomo de Tesla", "index": 1 },
            { "image": "/assets/sistemas-inteligentes-2.jpeg", "quoted": "Sistema de Visión Artificial", "index": 2 },
            { "image": "/assets/sistemas-inteligentes-3.jpg", "quoted": "Sistemas de Análisis de datos", "index": 3 }
          ],
          "details": "Desde 1995, ha habido un auge en el desarrollo de sistemas inteligentes, incluyendo robots autónomos, sistemas de visión artificial y algoritmos avanzados para el análisis de datos. Los sistemas inteligentes están cada vez más presentes en la vida cotidiana, desde asistentes de voz hasta robots industriales."
        }
      ]

    }
  },
  methods: {
    openModal(event: any) {
      this.selectedEvent = event;
      this.isModalVisible = true;
    },
    closeModal() {
      this.isModalVisible = false;
    },
    closeAuthorModal() {
      this.isAuthorModalVisible = false;
    }
  }
};
</script>

<style scoped>
/* Estilos para el modal de autor */
</style>
