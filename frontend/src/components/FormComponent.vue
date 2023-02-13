<template>
 <div class="">
    <form  class="bg-white shadow-md rounded px-8 pt-6 pb-8 divide-y-2 divide-solid divide-gray-300 flex flex-col space-y-4">
        <!--Name and Contact-->
        <div class="mb-5">
            <div class="flex mb-4 gap-4 w-full">
                <div class="w-full">
                    <label class="block text-gray-600 font-bold text-left text-sm" for="name">
                    First Name
                    </label>
                    <input  v-model="cv_data.firstname" class="shadow appearance-none border border-gray-300 rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" id="name" type="text" placeholder="John" maxlength="12">
                </div>
                <div class="w-full">
                    <label class="block text-gray-600 font-bold text-left text-sm" for="name">
                    Last Name
                    </label>
                    <input  v-model="cv_data.lastname" class="shadow appearance-none border border-gray-300 rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" id="name" type="text" placeholder="Doe"  maxlength="12">
                </div>

            </div>
            <div class="">
                <div class="mb-4">
                    <label class="block text-gray-600 font-bold text-left text-sm" for="name">
                    Telephone
                    </label>
                    <input v-model="cv_data.telephone"  class="shadow appearance-none border border-gray-300 rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" id="name" type="tel" placeholder="Telephone">
                </div>
                <div class="mb-4">
                    <label class="block text-gray-600 font-bold text-left text-sm" for="name">
                    Email
                    </label>
                    <input v-model="cv_data.email" class="shadow appearance-none border border-gray-300 rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" id="name" type="email" placeholder="Email">
                </div>
                <div class="">
                    <label class="block text-gray-600 font-bold text-left text-sm" for="name">
                    Website or Github
                    </label>
                    <input v-model="cv_data.link1" class="shadow appearance-none border border-gray-300 rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" id="name" type="tel" placeholder="URL">
                </div>
              
            </div>
        </div>
        <!-- Address -->
        <div class="">
            <div class="mb-4 mt-4">
                <div class="mb-4">
                    <label class="block text-gray-600 font-bold text-left text-sm" for="name">
                    Address
                    </label>
                    <input  v-model="cv_data.addressline1" class="shadow appearance-none border border-gray-300 rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" id="name" type="text" placeholder="Address Line 1">
                </div>
                <div class="mb-4">
                    <input v-model="cv_data.addressline2" class="shadow appearance-none border border-gray-300 rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" id="name" type="text" placeholder=" Address Line 2">
                </div>
                <div class="flex mb-4 gap-4 w-full">
                <div class="w-full">
                    <input v-model="cv_data.city" class="shadow appearance-none border border-gray-300 rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" id="name" type="text" placeholder="City">
                </div>
                <div class="w-full">
                    <input v-model="cv_data.postcode" class="shadow appearance-none border border-gray-300 rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" id="name" type="text" placeholder="Postcode">
                </div>

            </div>
           
              
            </div>
        </div>
        <!-- Profile Summary -->
        <div>
            <div class="mt-4 mb-4">
                <div class="mb-4">
                    <label class="block text-gray-600 font-bold text-left text-sm" for="name">
                    Profile Summary
                    </label>
                    <textarea v-model="cv_data.profilesummary" :maxlength="summaryMaxCount" class="shadow h-28 appearance-none border border-gray-300 rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" id="name" type="tel" placeholder="Summary..."></textarea>
                    <p class="text-left text-xs ext-gray-600 ">Characters left: {{ summaryMaxCount - summaryCount }}</p>
                </div>
            </div>
        </div>
        <!-- Skills -->
        <div>
            <div class="mt-4">
                <div class="mb-4">
                    <label class="block text-gray-600 font-bold text-left text-sm" for="name">
                    Skills
                    </label>
                    <input  class="shadow appearance-none border border-gray-300 rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" id="name" type="tel" placeholder="Skill">
                </div>
            </div>
            
        </div>
        <a class="cursor-pointer bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded" @click="emit_download_pdf">Download PDF</a>
    </form>
  </div>

</template>

<script>
export default {
    name: "FormComponent",
    watch : {
        'cv_data.firstname' : function(){
            this.emit_cv_data()
        },
        'cv_data.lastname' : function(){
            this.emit_cv_data()
        },
        'cv_data.telephone' : function(){
            this.emit_cv_data()
        },
        'cv_data.email' : function(){
            this.emit_cv_data()
        },
        'cv_data.link1' : function(){
            this.emit_cv_data()
        },
        'cv_data.addressline1' : function(){
            this.emit_cv_data()
        },
        'cv_data.addressline2' : function(){
            this.emit_cv_data()
        },
        'cv_data.city' : function(){
            this.emit_cv_data()
        },
         'cv_data.postcode' : function(){
            this.emit_cv_data()
        },
        'cv_data.profilesummary' : function(){
            this.emit_cv_data()
            this.countCharacters()
            // Observe word count
            this.updateSummaryLayout()
           
        },
        deep: true
    },
    data(){
        return {
            // Character Counter
            summaryMaxCount : 625,
            summaryCount: 0,
            summaryWordLineCount: 0,
            summaryCharacterLineCount: 0,
            cv_data : {
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
            }
        }
    },
    methods:{
        countCharacters(){
            console.log('count')
            this.summaryCount = this.cv_data.profilesummary.length
        },
        countWordsPerLine(){
            const maxNumberOfCharactersPerLine = 10;
            
            // Split text into lines array
            let lines = this.cv_data.profilesummary.split('\n');
            // Get the last and current line array
            let words = lines.at(-1).split(' ');
            // Assign current word count
            this.summaryWordLineCount = words.length
            // Check if word count is greater or equal to max word count
            if(this.summaryCharacterLineCount > maxNumberOfCharactersPerLine ){
                // get the second last word and add a \n line break
                this.cv_data.profilesummary.split(' ').at(-2)  
                console.log(this.cv_data.profilesummary.split(' ').at(-2))
                this.summaryCharacterLineCount = 0
            }
        },
        handleInput() {
            let maxRows = 6;
            let maxChars = 10;
            let lines = this.cv_data.profilesummary.split("\n");
            let newLines = [];

      for (let i = 0; i < lines.length; i++) {
        let line = lines[i];
        let lineStart = 0;
        while (line.length > maxChars) {
          let lastSpace = line.lastIndexOf(" ", lineStart + maxChars);
          let newLine = line.substring(lineStart, lastSpace);
          newLines.push(newLine);
          lineStart = lastSpace + 1;
          line = line.substring(lineStart);
        }
        newLines.push(line);
        if (newLines.length >= maxRows) break;
      }

      this.cv_data.profilesummary = newLines.join("\n");
    },
        updateSummaryLayout(){
            let maxRows = 7;
            let maxChars = 90;
            let lines = this.cv_data.profilesummary.split("\n");
            let newLines = [];
            
                for (let i = 0; i < lines.length; i++) {
                    console.log(i)
                    let line = lines[i];
                    let lineStart = 0;
                    while (line.length > maxChars) {
                        console.log("testing infinte")
                        let lastSpace = line.lastIndexOf(" ", lineStart + maxChars);
                        if (lastSpace === -1) {
                            lastSpace = lineStart + maxChars;
                        }
                        let newLine = line.substring(lineStart, lastSpace);
                        newLines.push(newLine);
                        lineStart = lastSpace + 1;
                        line = line.substring(lineStart);
                        }
                        newLines.push(line);
                        if (newLines.length >= maxRows) break;
                    }
                
                this.cv_data.profilesummary = newLines.join("\n");
            
                },

        emit_cv_data : function(){
            this.$emit('cv-data-emitted',this.cv_data)
        },
        emit_download_pdf : function(){
            this.$emit('download-pdf-emitted')
        }
    }
}
</script>

<style scoped>

</style>