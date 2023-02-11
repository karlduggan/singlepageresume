<template>
  <div class="app">
    <div class="tools overflow-auto">
      <FormComponent @cv-data-emitted="test" @download-pdf-emitted="downloadToPDF"></FormComponent>
    </div>
    <div class="preview bg-[#495163]">
      <canvas class="drop-shadow-lg" id="document" style="border-radius:5px"></canvas>
    </div>
  </div>
</template>

<script>
import FormComponent from './components/FormComponent.vue';
import preset from './presetstyle.json'
import { jsPDF } from "jspdf";

export default {
  name: 'App',
  components: {
    FormComponent
  },
  data() {
    return {
      selectedPreset : "preset01",
      presetstyle : preset,
      paperWidth: 595 ,
      paperHeight: 842 ,
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
      dataToPDF: [],
      pdfWidth : null,
      pdfHeight : null,
      // Emitted Data leave empty to avoid undefine displayed 
      cv_data : 
      {
        firstname : "First",
        lastname : "Last",
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
      // Setup data for PDF from inputs entries 
      this.setupPdfData()
      // Create jsPDF doc
      // width: 595.28px height: 841.89px
      var doc = new jsPDF('p', 'pt', 'a4') 
      // dataToPDF contains a list of objects containing text data
      // Iterate through the list of text data of dictionaries 
      // Example: {'text','fontStyle': 'Arial', 'fontSize': 24, 'fontColor': [225,0,0], 'xpos': 100, 'ypos': 100, 'textAlign': 'center'}
      for(var index = 0; index < this.dataToPDF.length; index++){
        doc.setFont(this.dataToPDF[index].fontStyle);
        doc.setFontSize(this.dataToPDF[index].fontSize);
        let rgb = this.dataToPDF[index].fontColor
        doc.setTextColor(rgb[0],rgb[1],rgb[2]);//RGB values
        // Offset needed to horizontally and vertically center so to match the preview 
        const x_offset = 0
        const y_offset = -6
        doc.text(this.dataToPDF[index].text, 
        this.dataToPDF[index].xpos + x_offset, 
        this.dataToPDF[index].ypos + y_offset, 
        this.dataToPDF[index].textAlign)
    }
      //doc.save('my-cv.pdf'); to save 
      window.open(doc.output('bloburl')); // to debug
    },
    setupPdfData(){
      // Goes through all inputs and if completed pushes to dataToPDF list 
      let header_name =  this.dataEntry(this.cv_data.firstname + " " + this.cv_data.lastname,'heading_01')
      let testData1 =  this.dataEntry(this.cv_data.firstname + " " + this.cv_data.lastname,'heading_02')
      let testData2 =  this.dataEntry(this.cv_data.firstname,'base','SummaryBase')
      this.dataToPDF.push(header_name)
      this.dataToPDF.push(testData1)
      this.dataToPDF.push(testData2)
    },
    dataEntry(text,textStyle){
      let data = {
        'text': text,
        'fontStyle': 'Helvetica', 
        'fontSize': this.presetstyle[this.selectedPreset][textStyle].fontSize, 
        'fontColor': this.presetstyle[this.selectedPreset][textStyle].fontColor, 
        'textAlign': this.presetstyle[this.selectedPreset][textStyle].textAlign,
        'xpos': this.presetstyle[this.selectedPreset][textStyle].x, 
        'ypos': this.presetstyle[this.selectedPreset][textStyle].y
      }
      return data
    },
    //drawGraphicsToPDF(){},
    test(data){
      this.cv_data = data
      this.draw()
    },
    handleResize: function () {
      // Calculate new canvas size based on window
      this.setCanvasSize()
      // Redraw the canvas with the updated size
      this.draw();
    },
    setCanvasSize() {
      const dimension = document.querySelectorAll(".preview")[0].getBoundingClientRect();
      this.canvas.height = dimension.height * 0.9;
      this.canvas.width = ((this.paperWidth / this.paperHeight) * this.canvas.height);
      // Set Style
      this.canvas.style.height  = dimension.height * 0.9 + 'px';
      this.canvas.style.width = (this.paperWidth / this.paperHeight) *  this.canvas.height + 'px';
    },
    previewSequence : function(){
      let seq = [
      // firstname & lastname
      "firstname"
      // telephone 
      // email 
      // link1 
      // addressline1
      // addressline2
      // city 
      // postcode
      // profilesummary
    ]
    return seq

    },
    renderPreviewText() {
      this.ctx.fillStyle = "#000";
      // Calculate the font size based on the current canvas width and the paper width
      let fontSize = this.presetstyle[this.selectedPreset]['heading_01'].fontSize * (this.canvas.width / this.paperWidth) ;

      // Loop through buffer here parameters (text from input, layout type from json)
      this.ctx.font = fontSize + "px Arial";
      this.ctx.fontStyle = "bold";
      this.ctx.textAlign = this.presetstyle[this.selectedPreset]['heading_01'].textAlign;
      this.ctx.textBaseline = "bottom";
      let text = this.cv_data.firstname + " " + this.cv_data.lastname;
      // Calculate the text position based on the current canvas width and the paper width
      let x = this.presetstyle[this.selectedPreset]['heading_01'].x * (this.canvas.width / this.paperWidth) ;
      let y = this.presetstyle[this.selectedPreset]['heading_01'].y * (this.canvas.width / this.paperWidth) ;
      this.ctx.fillText(text, x, y);

    },
    //drawPreviewText(text,fontSize,fontStyle,fontColor,textAlign,textBaseline,xPos,yPos){
    // Text is parsed via the usr input or saved file and the other paramenters are from the presetSetup json file  

    //},
    draw() { 
      // Clear the canvas
      this.ctx.clearRect(0, 0, this.canvas.width, this.canvas.height);
      // Set the font style, size, and color
      this.ctx.fillStyle = '#ffffff';
      this.ctx.fillRect(0,0,this.canvas.width,this.canvas.height);
      this.renderPreviewText();
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
