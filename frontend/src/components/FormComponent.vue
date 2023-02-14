<template>
 <div class="">
    <form  class="bg-white shadow-md rounded px-8 pt-6 pb-8 flex flex-col space-y-4">
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
            <div class="mt-4 ">
                <div class="mb-4">
                    <label class="block text-gray-600 font-bold text-left text-sm" for="name">
                    Skills
                    </label>
                    <div class="flex">
                        <input v-model="skillsValue"  v-on:keyup.enter="addToList('skills')" maxlength="100" class="shadow appearance-none border border-gray-300 rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" id="name" type="tel" placeholder="Press enter to add value">
                        <p class="pl-4 py-2 text-gray-400 cursor-pointer">
                            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1" stroke-linecap="round" stroke-linejoin="round" class="feather feather-edit"><path d="M11 4H4a2 2 0 0 0-2 2v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2v-7"></path><path d="M18.5 2.5a2.121 2.121 0 0 1 3 3L12 15l-4 1 1-4 9.5-9.5z"></path></svg>
                        </p>
                    </div>
                    <p class="p-1 text-left text-gray-400 text-xs">{{ cv_data.skills.length}} out of {{ maxEntries }}</p>
                </div>
            </div>
            
        </div>
        <!-- Languages -->
        <div>
            <div class="mt-4 ">
                <div class="mb-4">
                    <label class="block text-gray-600 font-bold text-left text-sm" for="name">
                    Languages
                    </label>
                    <div class="flex">
                        <input v-model="languageValue"  v-on:keyup.enter="addToList('languages')" maxlength="100"  class="shadow appearance-none border border-gray-300 rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" id="name" type="tel" placeholder="Press enter to add value">
                        <p class="pl-4 py-2 text-gray-400 cursor-pointer">
                            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1" stroke-linecap="round" stroke-linejoin="round" class="feather feather-edit"><path d="M11 4H4a2 2 0 0 0-2 2v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2v-7"></path><path d="M18.5 2.5a2.121 2.121 0 0 1 3 3L12 15l-4 1 1-4 9.5-9.5z"></path></svg>
                        </p>
                    </div>
                    <p class="p-1 text-left text-gray-400 text-xs">{{ cv_data.languages.length}} out of {{ maxEntries }}</p>
                </div>
            </div>
        </div>
        <!-- Frameworks -->
        <div>
            <div class="mt-4 ">
                <div class="mb-4">
                    <label class="block text-gray-600 font-bold text-left text-sm" for="name">
                    Frameworks
                    </label>
                    <div class="flex">
                        <input v-model="frameworkValue" v-on:keyup.enter="addToList('frameworks')" maxlength="100"  class="shadow appearance-none border border-gray-300 rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" id="name" type="tel" placeholder="Press enter to add value">
                        <p class="pl-4 py-2 text-gray-400 cursor-pointer">
                            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1" stroke-linecap="round" stroke-linejoin="round" class="feather feather-edit"><path d="M11 4H4a2 2 0 0 0-2 2v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2v-7"></path><path d="M18.5 2.5a2.121 2.121 0 0 1 3 3L12 15l-4 1 1-4 9.5-9.5z"></path></svg>
                        </p>
                    </div>
                    <p class="p-1 text-left text-gray-400 text-xs">{{ cv_data.frameworks.length}} out of {{ maxEntries }}</p>
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
            // Skills Value
            skillsValue: "",
            // Languages Value 
            languageValue: "",
            // Framework Value
            frameworkValue: "",
            // Max entries for lists
            maxEntries : 5,
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
                profilesummary : "",
                // Lists
                skills : [],
                languages : [],
                frameworks : []
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
        addToList : function (listName){
           
            let selectedList;
            let value;
            switch(listName){
                case "skills":
                    selectedList = this.skills;
                    value = this.cv_data.skillsValue;
                    // Clear Entry
                    this.skillsValue = ""
                    break;
                case "languages":
                    selectedList = this.cv_data.languages;
                    value = this.languageValue;
                    // Clear Entry
                    this.languageValue = ""
                    break;
                case "frameworks":
                    selectedList = this.cv_data.frameworks
                    value = this.frameworkValue;
                    // Clear Entry
                    this.frameworkValue = ""
                    break;
            }
            // Check if max value has already been reached, if not then input data
            if(selectedList.length < this.maxEntries){
                // Add data to selected list
                selectedList.push(value)
            } else {
                // Give error message in input field
                switch(listName){
                case "skills":
                    this.skillsValue = "Max entry of " + this.maxEntries + " reached!"
                    break;
                case "languages":
                    this.languageValue = "Max entry of " + this.maxEntries + " reached!"
                    break;
                case "frameworks":
                    this.frameworkValue = "Max entry of " + this.maxEntries + " reached!"
                    break;
                }
            }
            
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