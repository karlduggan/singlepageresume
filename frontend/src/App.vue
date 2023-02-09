<template>
  <div class="app">
    <div class="tools overflow-auto">
      <FormComponent @cv-data-emitted="test"></FormComponent>
    </div>
    <div class="preview bg-[#495163]">
      <canvas class="drop-shadow-lg" id="document" style="border-radius:5px"></canvas>
      <button class="absolute" @click="downloadToPDF">Download</button>
    </div>
  </div>
</template>

<script>
import FormComponent from './components/FormComponent.vue';
import { jsPDF } from "jspdf";

export default {
  name: 'App',
  components: {
    FormComponent
  },
  data() {
    return {
      paperWidth: 2480,
      paperHeight: 3508,
      paperBaseFontSize: 6,
      paperHeaderFontSize : 24,
      paperMarginHorizontal: 9,
      paperMarginVertical: 9,
      canvas: null,
      ctx: null,
      canvasMarginHorizontal: 0,
      canvasMarginVertical: 0,
      canvasBaseFontSize: 0,
      rect: null,
      // Emitted Data leave empty to avoid undefine displayed 
      cv_data : 
      {
        firstname : "",
        lastname : "",
        telephone : "",
        email : "",
        link1 : "",
        addressline1 : "",
        addressline2 : "",
        city : "",
        postcode : "",
        profilesummary : ""
      },
      setup : {}
    };
  },
  watch: {
    // All input fields should be placed in the watch method so to update the canvas
    canvas : function(){
      this.setCanvasSize()
      this.draw()
    }
  },
  mounted() {
    // Hook up the canvas to vue
    this.canvas = document.getElementById("document");
    this.ctx = this.canvas.getContext("2d");
    this.rect = this.canvas.getBoundingClientRect();
    this.setCanvasSize();
    this.draw();
  },
  methods: {
    downloadToPDF : function(){
      // Canvas ratio
      const ratio = this.canvas.width / this.canvas.height
      // A4 dimensions in portrait orientation
      const a4Width = 210;
      const a4Height = 297;

      var imgData = this.canvas.toDataURL('image/png');
      var doc = new jsPDF({
       orientation: "portrait", // landscape or portrait
       unit: "mm",
       format: "a4"
      });
      var width = doc.internal.pageSize.getWidth();
      var height = doc.internal.pageSize.getHeight();
      doc.addImage(imgData, 'PNG', 0,0,a4Width,a4Height);
      doc.save('my-cv.pdf');
    },
    pxToMm : function(px) {
      var resolution = 96; // Default screen resolution
      return px / resolution * 25.4;
    },
    test(data){
      this.cv_data = data
      this.draw()
    },
    setCanvasSize() {
      const d = document.querySelectorAll(".preview")[0].getBoundingClientRect();
      this.canvas.height = d.height * 0.9;
      this.canvas.width = (this.paperWidth / this.paperHeight) * this.canvas.height;
      
      this.canvas.style.width = this.canvas.width;
      this.canvas.style.height = this.canvas.height;

      this.canvasMarginHorizontal =
        this.paperMarginHorizontal * (this.canvas.width / this.paperWidth);
      this.canvasMarginVertical =
        this.paperMarginVertical * (this.canvas.height / this.paperHeight);
      this.canvasBaseFontSize =
        this.paperBaseFontSize * (this.canvas.height / this.paperHeight);
    },
    writeName() {
      this.ctx.fillStyle = "#000";
      this.ctx.font = this.paperHeaderFontSize + "px Arial";
      this.ctx.fontStyle = "bold";
      this.ctx.textAlign = "center";
      this.ctx.textBaseline = "top";
      this.ctx.fillText(
        this.cv_data.firstname + " " + this.cv_data.lastname,
        this.canvas.width - this.canvas.width/2,
        this.canvasMarginVertical
      );
    },
    draw() {
      console.log('drawing');
      this.ctx.fillStyle = '#ffffff';
      this.ctx.fillRect(0,0,this.canvas.width,this.canvas.height);
      this.writeName();


    }
  }}
   
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.app {
  background: #ccc;
  width: 100%;
  height: 100%;
  display: flex;
}
.tools {
  width: 30vw;
  height: 100vh;

}
.preview {
  width: 70vw;
  height: 100vh;
  background: grey;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
}

</style>
