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
      scale : 0,
      selectedPreset : "preset01",
      presetstyle : preset,
      paperWidth: 595,
      paperHeight: 842 ,
      paperBaseFontSize: 0,
      paperHeaderFontSize : 25,
      paperMarginHorizontal: 9,
      paperMarginVertical: 9,
      canvas: null,
      canvasBoxSize : null,
      ctx: null,
      rect: null,
      dataToRender: [],
      pdfWidth : null,
      pdfHeight : null,
      // Emitted Data leave empty to avoid undefine displayed 
      cv_data : 
      {
        firstname : "First",
        lastname : "Last",
        telephone : "07568303809",
        email : "tester@email.co.uk",
        link1 : "www.github.com/tester",
        addressline1 : "Flat 11",
        addressline2 : "45 St Nicholas Road",
        city : "Brighton",
        postcode : "BN13LO",
        profilesummary : "",
        skills: ['1','2','3'],
        // Bullet point list used for
        lists: {
          list01: {
            name: "Skills",
            items : []
            },
          list02: {
            name: "",
            items : []
          },
          list03: {
            name: "",
            items : []
          }
        }
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
      // Create jsPDF doc
      // width: 595.28px height: 841.89px
      var doc = new jsPDF('p', 'pt', 'a4') 
      // dataToRender contains a list of objects containing text data
      // Iterate through the list of text data of dictionaries 
      // Example: {'text','fontStyle': 'Arial', 'fontSize': 24, 'fontColor': [225,0,0], 'xpos': 100, 'ypos': 100, 'textAlign': 'center'}
      for(var index = 0; index < this.dataToRender.length; index++){
        doc.setFont(this.dataToRender[index].fontStyle);
        doc.setFontSize(this.dataToRender[index].fontSize);
        let rgb = this.dataToRender[index].fontColor
        doc.setTextColor(rgb[0],rgb[1],rgb[2]);//RGB values
        // Offset needed to horizontally and vertically center so to match the preview 
        const x_offset = 0
        const y_offset = -6
        doc.text(this.dataToRender[index].text, 
        this.dataToRender[index].xpos + x_offset, 
        this.dataToRender[index].ypos + y_offset, 
        this.dataToRender[index].textAlign)
    }
      //doc.save('my-cv.pdf'); to save 
      window.open(doc.output('bloburl')); // to debug
    },

    dataEntry(text,textStyle,newLineOffSet){
      let data = {
        'text': text,
        'fontStyle': 'Helvetica', 
        'fontSize': this.presetstyle[this.selectedPreset][textStyle].fontSize, 
        'fontColor': this.presetstyle[this.selectedPreset][textStyle].fontColor, 
        'textAlign': this.presetstyle[this.selectedPreset][textStyle].textAlign,
        'xpos': this.presetstyle[this.selectedPreset][textStyle].x, 
        'ypos': this.presetstyle[this.selectedPreset][textStyle].y + newLineOffSet
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
      // Important to clear before every draw otherwise no updates occur 
      this.dataToRender = []
      // Goes through all inputs and if completed pushes to dataToRender list 
      // Name
      this.dataToRender.push(this.dataEntry(this.cv_data.firstname + " " + this.cv_data.lastname,'heading_01',0))
      // Profile
      var lines = this.cv_data.profilesummary.split('\n');
      var newLineOffSet = 0
      for (var i = 0; i < lines.length; i++) {
        this.dataToRender.push(this.dataEntry(lines[i],'Profile_Summary',newLineOffSet))
        newLineOffSet += 10
      }

      // Address
      this.dataToRender.push(this.dataEntry(this.cv_data.addressline1,'Address_Line1',0))
      this.dataToRender.push(this.dataEntry(this.cv_data.addressline2,'Address_Line2',0))
      this.dataToRender.push(this.dataEntry(this.cv_data.city,'Address_City',0))
      this.dataToRender.push(this.dataEntry(this.cv_data.postcode,'Address_Postcode',0))
      // Contact
      this.dataToRender.push(this.dataEntry(this.cv_data.telephone,'Contact_Tel',0))
      this.dataToRender.push(this.dataEntry(this.cv_data.email,'Contact_Email',0))
      this.dataToRender.push(this.dataEntry(this.cv_data.link1,'Url_Link01',0))
      // Labels
      if(this.cv_data.profilesummary.length > 0){
        this.dataToRender.push(this.dataEntry("PROFILE",'Label_Profile',0))
      }
      this.dataToRender.push(this.dataEntry("SOFT SKILLS",'Label_Soft_Skills',0))
      this.dataToRender.push(this.dataEntry("LANGUAGES",'Label_Languages',0))
      this.dataToRender.push(this.dataEntry("EXPERIENCE",'Label_Experiences',0))
      this.dataToRender.push(this.dataEntry("FRAMEWORKS",'Label_Frameworks',0))
      this.dataToRender.push(this.dataEntry("EDUCATION & CERTIFICATIONS",'Label_Education_Cert',0))
      this.dataToRender.push(this.dataEntry("PROJECTS",'Label_Projects',0))
      // Hacked the below part together, will require cleaning later 
      // Go through list01
      // Get list01 position
      let posX = 0
      for(let i = 0; i < this.cv_data.lists.list01.items.length; i++){
        let item = this.cv_data.lists.list01.items[i]
        this.dataToRender.push(this.dataEntry(item,'Items_List01',posX+=20))
      }
      // Go through list02
      posX = 0
      for(let i = 0; i < this.cv_data.lists.list02.items.length; i++){
        let item = this.cv_data.lists.list02.items[i]
        this.dataToRender.push(this.dataEntry(item,'Items_List02',posX+=20))
      }
      // Go through list03
      posX = 0
      for(let i = 0; i < this.cv_data.lists.list03.items.length; i++){
        let item = this.cv_data.lists.list03.items[i]
        this.dataToRender.push(this.dataEntry(item,'Items_List03',posX+=20))
      }
    },
    // Important as this is where we display text to the preview canvas
    renderPreviewText() {
      this.ctx.fillStyle = "#000";
      // Testing
      this.previewSequence()
      // Loop through buffer here parameters (text from input, layout type from json)
      for(var index = 0; index < this.dataToRender.length; index++){
        // Calculate the font size based on the current canvas width and the paper width
        let fontSize = this.dataToRender[index].fontSize * (this.canvas.width / this.paperWidth) ;
        this.ctx.font = fontSize + "px Arial";
        this.ctx.fontStyle = "bold";
        this.ctx.textAlign = this.dataToRender[index].textAlign;
        this.ctx.textBaseline = "bottom";
        // Canvas uses hex and not rgb but jsPDF used rgb so we use the rgbToHex converter below
        let rgb = this.dataToRender[index].fontColor;
        let hex = this.rgbToHex(rgb[0],rgb[1],rgb[2])
        this.ctx.fillStyle = "#" + hex;
        // Calculate the text position based on the current canvas width and the paper width
        let x = this.dataToRender[index].xpos * (this.canvas.width / this.paperWidth) ;
        let y = this.dataToRender[index].ypos * (this.canvas.width / this.paperWidth) ;
        this.ctx.fillText(this.dataToRender[index].text, x, y); 
      }  
    },
    rgbToHex(r, g, b) {
      return ((r << 16) | (g << 8) | b).toString(16).padStart(6, '0');
    },
    draw() { 
       // Clear the canvas
      this.ctx.clearRect(0, 0, this.canvas.width, this.canvas.height);
      
      this.ctx.fillStyle = '#ffffff';
      this.ctx.fillRect(0,0,this.canvas.width ,this.canvas.height );
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
