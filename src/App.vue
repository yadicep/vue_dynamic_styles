<script>
  export default {
    data() {
      return {
        backgroundColor: 'DarkSeaGreen', // Color inicial de fondo
        textColor: 'White', // Color inicial del texto
        showText: true, // Si se debe mostrar el texto
        borderWidth: 0, // Ancho del borde de la figura
        borderRadius: 90, // Radio del borde de la figura
        textContent: 'Awesome Vue.js', // Texto inicial dentro de la figura
        fontFamily: 'Arial', // Fuente inicial
        isOpaque: false, // Si es opaco o no
        fontSize: 'medium', // Tamaño de letra
        showFigure: true, // Controla la visibilidad de la figura
        fontFamilies: ['Arial', 'Cursive', 'Arial Black', 'Monospace', 'Fantasy', 'Tahoma', 'Courier'], // Arreglo para las fuentes
        fontSizes: [ // Arreglo para los tamaños de letra
          { label: 'Pequeño', value: 'small' },
          { label: 'Mediano', value: 'medium' },
          { label: 'Grande', value: 'large' }
        ]
      }
    },
    computed: {
      figureStyles() {    // Función que cambia los estilos originales de la figura (llamada en la línea 120)
        return {
          backgroundColor: this.backgroundColor,
          color: this.textColor,
          borderWidth: `${this.borderWidth}px`,
          borderRadius: `${this.borderRadius}px`,
          borderStyle: 'solid',
          borderColor: '#347171',
          fontFamily: this.fontFamily,
          fontSize: this.getFontSize()
        }
      }
    },
    methods: {
      getFontSize() {     // Función que cambia el tamaño de la letra según la opción seleccionada
        switch (this.fontSize) {
          case 'small': return '12px';
          case 'medium': return '18px';
          case 'large': return '26px';
          default: return '16px';
        }
      }
    }
  }
</script>

<template>
  <div id="app">
    <div class="border border-2 rounded-4 p-5 bg-white">
      <div class="row">

        <!-- PANEL PARA LA CONFIGURACIÓN DE LA FIGURA -->
        <div class="col-md-6">
          <div class="card p-3 text-white text-start panel rounded-0">

            <div class="mb-3">
              <label>Color de fondo</label>
              <input type="text" class="form-control form-select-sm m-0" v-model="backgroundColor">
              <div id="passwordHelpBlock" class="form-text text-end m-0 p-0">
                <a href="https://htmlcolorcodes.com/es/nombres-de-los-colores/" target="_blank" class="text-light">Guía de Colores</a>
              </div>
            </div>

            <div class="mb-3">
              <label>Color de texto</label>
              <input type="text" class="form-control form-select-sm m-0" v-model="textColor">
              <div id="passwordHelpBlock" class="form-text text-end m-0 p-0">
                <a href="https://htmlcolorcodes.com/es/nombres-de-los-colores/" target="_blank" class="text-light">Guía de Colores</a>
              </div>
            </div>

            <div class="position-relative mb-4">
              <div class="form-check form-check-reverse position-absolute start-0">
                <input type="checkbox" class="form-check-input" v-model="showText">
                <label>Mostrar texto</label>
              </div>
            </div><br>

            <div class="mb-3">
              <label>Ancho del borde</label>
              <input type="range" class="form-range" v-model="borderWidth" min="0" max="10">
              <label>Radio del borde</label>
              <input type="range" class="form-range" v-model="borderRadius" min="0" max="150">
            </div>

            <div class="mb-3">
              <label>Contenido textual</label>
              <input type="text" class="form-control form-select-sm" v-model="textContent">
            </div>

            <div class="mb-3">
              <label>Tipografía</label>
              <select class="form-select form-select-sm" v-model="fontFamily">
                <option v-for="(font, index) in fontFamilies" :key="index" :value="font">{{ font }}</option>  <!-- v-for para iterar el arreglo fontFamilies del estado -->
              </select>
            </div>

            <div class="position-relative my-4">
              <div class="form-check form-check-reverse position-absolute start-0">
                <label>Opaco</label>
                <input type="checkbox" class="form-check-input" v-model="isOpaque">
              </div>
            </div><br>

            <div class="mb-3">
              <label>Tamaño de letra</label>
              <div>
                <div class="form-check form-check-inline" v-for="(size, index) in fontSizes" :key="index">    <!-- v-for para iterar el arreglo fontSizes del estado -->
                  <input type="radio" class="form-check-input" :id="size.value" :value="size.value" v-model="fontSize">
                  <label :for="size.value" class="form-check-label">{{ size.label }}</label> 
                </div>
              </div>
            </div>

          </div>
        </div>

        <div class="col-md-1"></div>

        <!-- FIGURA PARA MOSTRAR LOS CAMBIOS DE ESTILO-->
        <div class="col-md-5 d-flex justify-content-center align-items-center">
          <!-- style binding para asignar estilos reactivamente --> 
          <!-- class binding para asignar clases reactivamente --> 
          <div :class="{'transparent-class': isOpaque, 'opaque-class': !isOpaque}" class="figure text-center" :style="figureStyles">  
            <div v-show="showText">{{ textContent }}</div>    <!--  v-show para mostrar u ocultar el texto -->
          </div>
        </div>

        <!-- 
        - La clase 'figure' la apliqué sólo para el estilo inicial de la figura con css
        - 'figureStyles' es la función para el cambio de estilos (definidos en la línea 24)
        - 'v-show' es la directiva para mostrar o no el texto (llamada en la línea 72) declarado inicialmente como true y modificado con el checkbox
        -->

      </div>
    </div>
  </div>
</template>

<style scoped>
  .figure {
    width: 300px;
    height: 300px;
    border-radius: 90px;
    text-align: center;
    display: flex;
    justify-content: center;
    align-items: center;
    transition: all 0.35s ease;
  }

  .panel {
    width: 500px;
    background-color: #154444;
  }

  .opaque-class {
    opacity: 1;
  }

  .transparent-class {
    opacity: 0.5;
  }
</style>