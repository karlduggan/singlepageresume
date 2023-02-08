<template>
  <div class="app">
  <div class="tools">
    <h3>Details</h3>
    <div class="field">
      <input v-model="companyNameField" type="text" id="name" placeholder="Company name" />
    </div>
    <div class="field">
      <textarea id="address" placeholder="Company address"></textarea>
    </div>
    </div>
    <div class="preview">
      <canvas id="document" style="border-radius:5px"></canvas>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  components: {
   
  },
  data() {
    return {
      paperWidth: 2480,
      paperHeight: 3508,
      paperBaseFontSize: 6,
      paperHeaderFontSize : 24,
      paperMarginHorizontal: 9,
      paperMarginVertical: 9,
      companyNameField: "",
      companyAddressField: "",
      canvas: null,
      ctx: null,
      canvasMarginHorizontal: 0,
      canvasMarginVertical: 0,
      canvasBaseFontSize: 0,
      rect: null

    };
  },
  watch: {
    // All input fields should be placed in the watch method so to update the canvas
    companyNameField : function(){
      console.log("draw")
      this.draw()
    },
    companyAddressField : function(){
      this.draw()
    },
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
    writeCompanyName() {
      this.ctx.fillStyle = "#000";
      this.ctx.font = this.paperHeaderFontSize + "px Arial";
      this.ctx.fontStyle = "bold";
      this.ctx.textAlign = "center";
      this.ctx.textBaseline = "hanging";
      this.ctx.fillText(
        this.companyNameField,
        this.canvas.width - this.canvas.width/2,
        this.canvasMarginVertical
      );
    },
    writeAddress() {
      this.ctx.fillStyle = "#000";
      this.ctx.font = this.canvasBaseFontSize + "px sans-serif";
      this.ctx.textAlign = "right";
      this.ctx.textBaseline = "hanging";
      this.companyAddressField.split("\n")
        .map((text, index) => {
          this.writeAddressLine(index + 1, text);
        });
    },
    draw() {
      console.log('drawing');
      this.ctx.fillStyle = '#ffffff';
      this.ctx.fillRect(0,0,this.canvas.width,this.canvas.height);
      this.writeCompanyName();
      this.writeAddress();
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
.field {
  margin: 1em 0;
  
  
}
</style>
