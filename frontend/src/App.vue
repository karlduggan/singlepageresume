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
      // !IMPORTANT! scale value must NOT change to maintain close to accurate text pixel sizes
      scale :  4.2,
      paperWidth: 2480 ,
      paperHeight: 3508,
      paperBaseFontSize: 0,
      paperHeaderFontSize : 25,
      paperMarginHorizontal: 9,
      paperMarginVertical: 9,
      canvas: null,
      canvasBoxSize : null,
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
    // Listen for the resize event on the window
    window.addEventListener("resize", this.handleResize);
    
  },
  beforeUnmount() {
      window.removeEventListener('resize', this.handleResize);
  },
  
  methods: {
    downloadToPDF : function(){
      // Scale up the canvas for high-res test
  


      var imgData = this.canvas.toDataURL('image/PNG', 1.0);

      var doc = new jsPDF({
       orientation: "portrait", // landscape or portrait
       unit: "px",
       format: "a4"
      });

      var width = doc.internal.pageSize.getWidth();
      var height = doc.internal.pageSize.getHeight();
    
      doc.addImage(imgData, 'PNG', 0,0,width,height);
      //doc.save('my-cv.pdf'); to save 
      window.open(doc.output('bloburl')); // to debug
 
    },
    test(data){
      this.cv_data = data
      this.draw()
    },
    handleResize: function () {
      // Calculate new canvas size based on window
      this.setCanvasSize()
      this.draw();
    },
    setCanvasSize() {
      const dimension = document.querySelectorAll(".preview")[0].getBoundingClientRect();
      this.canvas.height = dimension.height * 0.9;
      this.canvas.width = ((this.paperWidth / this.paperHeight) * this.canvas.height);
      console.log(dimension)
      // Set Style
      this.canvas.style.height  = dimension.height * 0.9 + 'px';
      this.canvas.style.width = (this.paperWidth / this.paperHeight) *  this.canvas.height + 'px';

      this.canvasMarginHorizontal =
        this.paperMarginHorizontal * (this.canvas.width / this.paperWidth);
      this.canvasMarginVertical =
        this.paperMarginVertical * (this.canvas.height / this.paperHeight);
      
      // !IMPORTANT! Font scales with this code 
      this.canvasBaseFontSize = this.paperBaseFontSize * (this.canvas.width / this.paperWidth);

    },
    writeName() {
      this.ctx.fillStyle = "#000";
      // !IMPORTANT! Font scales with this code 
      this.ctx.font = this.paperHeaderFontSize * (this.canvas.width / this.paperWidth) * this.scale + "px Arial";
      console.log(this.ctx.font)
      this.ctx.fontStyle = "bold";
      this.ctx.textAlign = "center";
      this.ctx.textBaseline = "top";
      let text = this.cv_data.firstname + " " + this.cv_data.lastname
      this.ctx.fillText(
        text,
        this.canvas.width - this.canvas.width/2,
        this.canvasMarginVertical
      );
      
    },

    draw() { 
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
